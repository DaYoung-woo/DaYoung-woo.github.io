---
layout: post
title: ReactQuery 사용 환경 설정
image:
excerpt: ReactQuery 사용 환경 설정
categories: REACT
category: REACT
tags: [REACT, ReactQuery, API, 리액트쿼리]
---

## 리액트쿼리(ReactQuery)

[tanstack ReactQuery](https://tanstack.com/query/v3)  
리액트 쿼리를 사용하면 정해진 시간동안 데이터를 캐싱하여 보여준다.  
캐싱된 데이터를 보여주다가 일정 시간이 경과되면 자동으로 데이터를 갱신해준다.  
변동이 잦지 않은 데이터의 경우 ReactQuery를 사용하면 네트워크 부하를 줄일 수 있다.

---

### 리액트쿼리 설치

#### npm 설치

{% highlight npm %}
$ npm i react-query
{% endhighlight %}

#### yarn 설치

{% highlight npm %}
$ yarn add react-query
{% endhighlight %}

#### cdn

{% highlight html %}

<script src="https://unpkg.com/react-query/dist/react-query.production.min.js"></script>

{% endhighlight %}

---

### /src/index.js 세팅

1. QueryClient, QueryClientProvider를 import한다.
2. new QueryClient를 사용하여 queryClient를 생성한다.
3. QueryClientProvider로 감싸준다.

{% highlight jsx %}
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import { RouterProvider } from "react-router-dom";
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
import { RecoilRoot } from "recoil";
import AppRouter from "./utils/router";
import "./index.scss";

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      cacheTime: 1000 * 60 * 5, // 5분 동안 캐시로 저장
      staleTime: 1000 * 60, // 1분 이내에는 캐시된 결과를 사용
    },
  },
});

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <QueryClientProvider client={queryClient}>
      <RecoilRoot>
        <RouterProvider router={AppRouter} />
      </RecoilRoot>
    </QueryClientProvider>
  </StrictMode>
);


{% endhighlight %}

---

### 컴포넌트에서 사용

{% highlight jsx %}
import { useState, useEffect } from "react";
import { ReactComponent as Trashbin } from "../../assets/img/trashbin.svg";
import { useQuery } from "@tanstack/react-query";
import { categoryListApi, categorySaveApi } from "../../api/api";
function CategoryList() {
  const [btnDisabled, setDisabled] = useState(true);
  const [year, setYear] = useState("");
  const [order, setOrder] = useState("");

  // 카테고리 리스트 api 요청
  const { status, data: categoryList } = useQuery({
    queryKey: ["fetchCategoryList"],
    queryFn: () => categoryListApi(),
  });

  return (
    <div>
      <div>
        {status === "pending" && (
          <div className="text-center mt-36">...loading</div>
        )}
        {status === "error" && (
          <div className="text-center mt-36">
            데이터를 가져오는데 실패했어요😭
          </div>
        )}
        {status === "success" && (
          <ul className="quiz-list pt-2">
            {!!categoryList &&
              categoryList.map(({ id, year, order }) => (
                <li className="hover:bg-slate-50 py-1" key={id}>
                  <div className="flex justify-between">
                    {year}년도 {order}회차
                  </div>
                  <Trashbin className="mr-2" height="16px" fill="#6B7280" />
                </li>
              ))}
            {!categoryList.length && (
              <div className="text-center mt-36">등록된 데이터가 없습니다</div>
            )}
          </ul>
        )}
      </div>
    </div>
  );
}

export default CategoryList;

{% endhighlight %}

---

{% highlight jsx %}
  // 카테고리 리스트 api 요청
  const { status, data: categoryList } = useQuery({
    queryKey: ["fetchCategoryList"],
    queryFn: () => categoryListApi(),
  });
{% endhighlight %}

페이지가 로드되면 아래의 queryFn에 정의된 메서드가 실행된다.  
status로 api호출에 대한 정보를 알 수 있다.  
- pending: api 요청중
- success: api 요청 성공
- error: api 요청 실패  

status 상태에 따라 사용자에게 보여줄 ui를 분기 처리해주었다.

{% highlight jsx %}
{status === "pending" && (
  <div className="text-center mt-36">...loading</div>
)}
{status === "error" && (
  <div className="text-center mt-36">
    데이터를 가져오는데 실패했어요😭
  </div>
)}
{status === "success" && (
  <ul className="quiz-list pt-2">
    {!!categoryList &&
      categoryList.map(({ id, year, order }) => (
        <li className="hover:bg-slate-50 py-1" key={id}>
          <div className="flex justify-between">
            {year}년도 {order}회차
          </div>
          <Trashbin className="mr-2" height="16px" fill="#6B7280" />
        </li>
      ))}
    {!categoryList.length && (
      <div className="text-center mt-36">등록된 데이터가 없습니다</div>
    )}
  </ul>
)}
{% endhighlight %}

data 정보에 api호출로 받은 값이 들어가게 된다.  
내가 호출한 값은 리스트로 돌아와서 map을 통해 뿌려줬다.


[ReactQuery를 적용하여 만든 미니 프로젝트](https://github.com/DaYoung-woo/linux-quiz)  
# 책 검색 웹사이트 Book-Searcher
![bookSearcher main](https://user-images.githubusercontent.com/74494210/162439119-087b9210-9dd9-48ef-b21c-6b9bfb904da3.png)

Demo : https://netkro-0706.github.io/Book-Searcher/

## 개발목표  
원하는 책을 찾을 수 있는 웹사이트를 개발  
API와 pagination을 이해하여 그 기술을 이용한 웹사이트 구축

## 사용기술
HTML  
CSS  
Javascript  
Bootstrap  
Font Awesome  
API - [Kakao Developers -> search-book](https://developers.kakao.com/docs/latest/ko/daum-search/dev-guide#search-book)

## 기능
+ 미디어 쿼리를 이용하여 화면 크기별로 UI가 변하여 보이도록 반응형 웹페이지를 구현  
  PC  
  ![bookSearcher main_sizing](https://user-images.githubusercontent.com/74494210/162488628-2e47c692-0c0d-4001-b573-68df4b3f90c7.png)  
  Tablet  
  ![bookSearcher tabsizing](https://user-images.githubusercontent.com/74494210/162489043-b3f301b6-d358-41c0-9d25-db9513a53e85.png)  
  Phone  
  ![bookSearcher phonesizing](https://user-images.githubusercontent.com/74494210/162489060-2296ace4-a138-4746-9ea7-dd18b932cd23.png)  

```css
@media (max-width: 768px) {
    body{
        max-width: 100%;
    }
    body *{
        max-width: 100%;
    }
    .main-wrap{
        width: 100%;
        min-width: auto;
    }
    .header-img-wrap, .carousel{
        display: none;
    }
    .center-wrap{
        margin-top: 20px;
    }
    .title-wrap h2{
        font-size: 60px;
    }
    .search-ipt{
        min-width: 170px;
        width: 275px;
    }

    .book-wrap{
        width: 90%;
        margin: 0 auto;
    }
    .book-detail{
        width: 590px;
    }
    .book-img{
        margin: auto;
    }
  }
  ...
```
+ API의 목록을 페이지 별로 보여지도록 Pagination 구현  
  ![pagination](https://user-images.githubusercontent.com/74494210/162561173-5d24f6bf-eefa-4c37-8cf7-a2b494088231.png)

```javascript
  ...
  pageNationHTML = `
            <li class="page-item ${nowPage <= 3 || lastPage <= 5 ? "display-none" : ""}">
                <a class="page-link" href="#" aria-label="Previous" onclick="pageMove(1)">
                  <span aria-hidden="true">&laquo;</span>
                </a>
            </li>
            <li class="page-item ${nowPage == 1 ? "display-none" : ""}">
                <a class="page-link" href="#" aria-label="Previous" onclick="pageMove(page-1)">
                  <span aria-hidden="true">&lt;</span>
                </a>
            </li>`

    for (firstPage; firstPage<=lastPage; firstPage++) {
        if(firstPage>last_group_page){
            break;
        }
        pageNationHTML += `
                    <li class="page-item"><a class="page-link" href="#" onclick="pageMove(${firstPage})">${firstPage}</a></li>
                    `
    }

    pageNationHTML += `
            <li class="page-item ${nowPage == last_group_page ? "display-none" : ""}">
                <a class="page-link" href="#" aria-label="Next" onclick="pageMove(page+1)">
                  <span aria-hidden="true">&gt;</span>
                </a>
            </li>
            <li class="page-item ${nowPage >= first_group_page || firstPage == 1 ? "display-none" : ""}">
                <a class="page-link" href="#" aria-label="Next" onclick="pageMove(${last_group_page})">
                    <span aria-hidden="true">&raquo;</span>
                </a>
            </li>
      `;
```

## 개선사항
API문제로 페이지의 최대값이 현재페이지의 위치에 따라 변동되는 문제가 발생중 -> 실시간으로 변동되는 최대페이지 값에 유연하게 맞출 수 있는 대응이 필요  
 ex)현재페이지 기준으로 5개 페이지 구현시 마지막에 중복된 페이지가 연달아 표시됨
<br/><br/>API와 받은 meta값을 좀 더 분석 및 조합하여 필터에 가격내림차순, 가격오름차순, 판매상태순의 구현이 필요

# 本検索ページ Book-Searcher
![main](https://user-images.githubusercontent.com/74494210/167297159-79021dbc-5747-446f-be45-ea2550073f99.png)

Demo : https://netkro-0706.github.io/Book-Searcher_JP/

## 開発目標  
探したい本を探せるWEBを開発  
APIとpaginationを理解しその技術を利用したWEBを構築

## 使用技術
HTML  
CSS  
Javascript  
Bootstrap  
Font Awesome  
API - [Kakao Developers -> search-book](https://developers.kakao.com/docs/latest/ko/daum-search/dev-guide#search-book)

## 機能기능
+ メディアクエリーを利用し画面の大きさに合わせてUIが変わるよう反応方WEBを具現  
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
+ APIの目録をページ別に見えるようにPagination具現  
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

## 改選項目
APIの問題でページの最大値が現在ページの位置によって変わる問題が発生中->実時間に変化する最大値に悠然合わせる対応が必要
 ex)現在ページの基準で5のページ具現時最後に中腹するページが続いて表示される
<br/><br/>APIと受けたmeta値をもっと分析、総合してフィルターに価格順、販売状態準などの具現が必要

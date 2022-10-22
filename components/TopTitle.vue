<template>
    <div class="TopTitle">
        <h1>
            都道府県別の総人口推移グラフ
        </h1>
    </div>
</template>
<style>
.TopTitle h1 {
    background-color: #C0C0C0; 
    padding: 30px 0;
    text-align: center;
}
/*phone*/
@media screen and (max-width: 480px) {
    .TopTitle h1 {
        font-size: 15px;
    }
}
/*タブレット*/
@media screen and (min-width: 481px) and (max-width: 959px) {
    .TopTitle h1 {
        font-size: 25px;
    }
}
/*pc*/
@media screen and (mix-width: 960px) {
    .TopTitle h1 {
        font-size: 30px;
    }
}
</style>
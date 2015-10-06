# 目標
使用Angular UI來實作dropdown
Angular技巧, 我要將此段程式寫成一個樣本, 首先自訂directive
```javascript
app.directive('pageHeader', function () {
    return {
        restrict: 'C',
        templateUrl:'page-header.html'
    };
});
```
就可以用
```html
<div class="page-header"></div>
```
要寫在同一個網頁裡可用ng-template來包
```html
   <script type="text/ng-template" id="page-header.html">
   </script>
```
載入函式庫
```html
<link href="~/Content/bootstrap.min.css" rel="stylesheet" />
<script src="~/Scripts/angular.min.js"></script>
<script src="~/Scripts/angular-ui/ui-bootstrap.min.js"></script>
```
可放在實體檔或ng-template裡
```html
<div dropdown>
     <button type="button" class="btn btn-default" dropdown-toggle>
         我的最愛
         <span class="caret"></span>
     </button>
     <ul class="dropdown-menu">
         <li><a href="https://www.google.com.tw/" target="_blank">Google</a></li>
         <li><a href="http://getbootstrap.com/" target="_blank">Bootstrap</a></li>
         <li><a href="https://angularjs.org/" target="_blank">AngularJS</a></li>
         <li class="divider"></li>
         <li><a href="http://caniuse.com/" target="_blank">Can i user</a></li>
     </ul>
 </div>
```
原bootstrap
```html
<link href="~/Content/bootstrap.min.css" rel="stylesheet" />
<script src="~/Scripts/jquery-1.9.1.min.js"></script>
<script src="~/Scripts/bootstrap.min.js"></script>
```
```html
<div class="dropdown">
    <button class="btn btn-default" type="button" data-toggle="dropdown">
        Dropdown1
        <span class="caret"></span>
    </button>
    <ul class="dropdown-menu">
        <li><a href="https://www.google.com.tw/" target="_blank">Google</a></li>
            <li><a href="http://getbootstrap.com/" target="_blank">Bootstrap</a></li>
            <li><a href="https://angularjs.org/" target="_blank">AngularJS</a></li>
            <li class="divider"></li>
            <li><a href="http://caniuse.com/" target="_blank">Can i user</a></li>
    </ul>
</div>
```
異差只有兩處
```
angularUI <div dropdown>
bootstrap <div class="dropdown">
angularUI <button dropdown-toggle>
bootstrap <button data-toggle="dropdown">
```
dropdown是做選單用的,在HTML的combobox是select
```html
<select ng-model="selected" ng-init="selected=items[0]" ng-options="item.value for item in items" ng-change="openUrl()"></select>
```
```javascript
app.controller('pageController',
  function ($scope) {
    $scope.openUrl = function() {
      window.open($scope.selected.key, "new_win");
    };
  }
);
```

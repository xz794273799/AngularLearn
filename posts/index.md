<!DOCTYPE html>
<html>
<head>
<title>朱回的Angular4+学习之旅</title>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
<script type="text/javascript">
 //是否显示导航栏
 var showNavBar = true;
 //是否展开导航栏
 var expandNavBar = true;

 $(document).ready(function(){
    var h1s = $("body").find("h1");
    var h2s = $("body").find("h2");
    var h3s = $("body").find("h3");
    var h4s = $("body").find("h4");
    var h5s = $("body").find("h5");
    var h6s = $("body").find("h6");

    var headCounts = [h1s.length, h2s.length, h3s.length, h4s.length, h5s.length, h6s.length];
    var vH1Tag = null;
    var vH2Tag = null;
    for(var i = 0; i < headCounts.length; i++){
        if(headCounts[i] > 0){
            if(vH1Tag == null){
                vH1Tag = 'h' + (i + 1);
            }else{
                vH2Tag = 'h' + (i + 1);
            }
        }
    }
    if(vH1Tag == null){
        return;
    }

    $("body").prepend('<div class="BlogAnchor">' + 
        '<span style="color:red;position:absolute;top:-6px;left:0px;cursor:pointer;" onclick="$(\'.BlogAnchor\').hide();">×</span>' +
        '<p>' + 
            '<b id="AnchorContentToggle" title="收起" style="cursor:pointer;">目录▲</b>' + 
        '</p>' + 
        '<div class="AnchorContent" id="AnchorContent"> </div>' + 
    '</div>' );

    var vH1Index = 0;
    var vH2Index = 0;
    $("body").find("h1,h2,h3,h4,h5,h6").each(function(i,item){
        var id = '';
        var name = '';
        var tag = $(item).get(0).tagName.toLowerCase();
        var className = '';
        if(tag == vH1Tag){
            id = name = ++vH1Index;
            name = id;
            vH2Index = 0;
            className = 'item_h1';
        }else if(tag == vH2Tag){
            id = vH1Index + '_' + ++vH2Index;
            name = vH1Index + '.' + vH2Index;
            className = 'item_h2';
        }
        $(item).attr("id","wow"+id);
        $(item).addClass("wow_head");
        $("#AnchorContent").css('max-height', ($(window).height() - 180) + 'px');
        $("#AnchorContent").append('<li><a class="nav_item '+className+' anchor-link" onclick="return false;" href="#" link="#wow'+id+'">'+name+" · "+$(this).text()+'</a></li>');
    });

    $("#AnchorContentToggle").click(function(){
        var text = $(this).html();
        if(text=="目录▲"){
            $(this).html("目录▼");
            $(this).attr({"title":"展开"});
        }else{
            $(this).html("目录▲");
            $(this).attr({"title":"收起"});
        }
        $("#AnchorContent").toggle();
    });
    $(".anchor-link").click(function(){
        $("html,body").animate({scrollTop: $($(this).attr("link")).offset().top}, 500);
    });

    var headerNavs = $(".BlogAnchor li .nav_item");
    var headerTops = [];
    $(".wow_head").each(function(i, n){
        headerTops.push($(n).offset().top);
    });
    $(window).scroll(function(){
        var scrollTop = $(window).scrollTop();
        $.each(headerTops, function(i, n){
            var distance = n - scrollTop;
            if(distance >= 0){
                $(".BlogAnchor li .nav_item.current").removeClass('current');
                $(headerNavs[i]).addClass('current');
                return false;
            }
        });
    });

    if(!showNavBar){
        $('.BlogAnchor').hide();
    }
    if(!expandNavBar){
        $(this).html("目录▼");
        $(this).attr({"title":"展开"});
        $("#AnchorContent").hide();
    }
 });
</script>
<style>
    /*导航*/
    .BlogAnchor {
        background: #f1f1f1;
        padding: 10px;
        line-height: 180%;
        position: fixed;
        right: 48px;
        top: 48px;
        border: 1px solid #aaaaaa;
    }
    .BlogAnchor p {
        font-size: 18px;
        color: #15a230;
        margin: 0 0 0.3rem 0;
        text-align: right;
    }
    .BlogAnchor .AnchorContent {
        padding: 5px 0px;
        overflow: auto;
    }
    .BlogAnchor li{
        text-indent: 0.5rem;
        font-size: 14px;
        list-style: none;
    }
    .BlogAnchor li .nav_item{
        padding: 3px;
    }
    .BlogAnchor li .item_h1{
        margin-left: 0rem;
    }
    .BlogAnchor li .item_h2{
        margin-left: 2rem;
        font-size: 0.8rem;
    }
    .BlogAnchor li .nav_item.current{
        color: white;
        background-color: #5cc26f;
    }
    #AnchorContentToggle {
        font-size: 13px;
        font-weight: normal;
        color: #FFF;
        display: inline-block;
        line-height: 20px;
        background: #5cc26f;
        font-style: normal;
        padding: 1px 8px;
    }
    .BlogAnchor a:hover {
        color: #5cc26f;
    }
    .BlogAnchor a {
        text-decoration: none;
    }
</style>

</head>
<body>
## 欢迎来到朱回的Angular4+学习之旅 ##
### 前言 ###
我是一名在互联网行业从事Java开发的软件工程师，具备多年互联网及电商平台的开发经验，本文撰写的主要目的是总结平时工作的过程中对前端Angular框架的学习和使用
### 前端开源UI框架收录 ###
<table>
<tr><td>项目名称</td><td>项目介绍</td><td>地址</td><td>JS框架支持</td></tr>
<tr><td>Boostrap</td><td>来自 Twitter,是目前最受欢迎的前端UI框架</td><td>官网：https://getbootstrap.com/<br/>中文网：http://www.bootcss.com/</td><td> </td></tr>
<tr><td>ng-bootstap</td><td>基于Bootstrap 4 CSS的angular组件库</td><td>Github Pages：https://ng-bootstrap.github.io/</td><td>Angular</td></tr>
<tr><td>ngx-bootstrap</td><td>Native Angular directives for Bootstrap</td><td>官网：https://valor-software.com/ngx-bootstrap/</td><td>Angular</td></tr>
<tr><td>ag-grid</td><td>企业级风格数据表格组件，如排序、过滤、自定义渲染、编辑、分组、聚合和旋转。</td><td>官网：https://www.ag-grid.com/<br/>Angular：https://www.ag-grid.com/angular-getting-started/</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>amexio</td><td>平台级Angular UI。开放源代码（Apache 2许可证）免费，并由Meta MaungEnglobal公司支持。<br/>120+ UI Widgets<br/>Drag & Drop Widgets<br/>Responsive Web Design<br/>57 Material Design Themes<br/>Charts / Maps / Dashboard / Layouts</td><td>官网：https://amexio.tech/<br/>API：http://api.amexio.tech/<br/>DEMO: http://demo.amexio.tech/<br/>源码：https://github.com/meta-magic/amexio.github.io</td><td>Angular</td></tr>
<tr><td>Material</td><td>Google I/O 2014 发布的 Material Design 统一 Android Mobile、Android Table、Desktop Chrome 等全平台设计语言规范</td><td>官网：https://material-ui.com/<br/>中文网：http://design.1sters.com<br/>Angular Material:https://material.angular.io/</td><td>Reat/Angular</td></tr>
<tr><td>Clarity Design System</td><td>UI框架 Angular组件库</td><td>Github Pages：https://vmware.github.io/clarity/</td><td>Angular</td></tr>
<tr><td>DevExtreme</td><td>50 + UI组件，包括数据网格、枢轴网格、调度器、图表、编辑器、地图和其他多用途控件，用于为触摸设备和传统桌面创建高度响应的Web应用程序。</td><td>官网：https://js.devexpress.com/<br/>Angular: https://js.devexpress.com/Overview/Angular/<br/>API: https://js.devexpress.com/Documentation/<br/>源码：https://github.com/DevExpress/devextreme-angular#adding-devexteme-to-an-existing-angular-application</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>element UI</td><td>Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库，来自于饿了么</td><td>官网：http://element-cn.eleme.io/<br/>Angular: https://element-angular.faas.ele.me/</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>Essential</td><td>企业级应用 web, mobile, and desktop applications<br/>800+UI组件、看板、图表<br/>45+ ANGULAR COMPONENTS</td><td>官网：https://www.syncfusion.com/<br/>Angular:https://www.syncfusion.com/products/angular</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>jQWidgets</td><td>平台级UI<br/>包括数据网格、树形网格、枢轴网格、调度器、图表、编辑器和其他多用途组件的角度UI组件</td><td>官网：https://www.jqwidgets.com/<br/>Demo: https://www.jqwidgets.com/jquery-widgets-demo/<br/>Angular：https://www.jqwidgets.com/angular/</td><td>Angular/Reat</td></tr>
<tr><td>Kendo UI</td><td>第一个支持Angular的主要平台级UI<br/>组件丰富，可构建原始app，响应式Web</td><td>官网：https://www.telerik.com/<br/>Angular: https://www.telerik.com/kendo-angular-ui/</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>Ignite UI</td><td>拥有强大的Data Grid、Data Charts，和其他丰富的组件</td><td>官网：https://www.infragistics.com/<br/>Angular:https://www.infragistics.com/products/ignite-ui-angular</td><td>Angular</td></tr>
<tr><td>ng-lightning</td><td>Native Angular components & directives for Lightning Design System</td><td>Github Pages：http://ng-lightning.github.io/ng-lightning/</td><td> </td></tr>
<tr><td>Ant Design</td><td>蚂蚁金服的一个服务于企业级产品的设计体系UI</td><td>官网：https://ant.design/index-cn<br/>Reat：https://ant.design/docs/react/introduce-cn<br/>Angular（NG-ZORROR）：https://ng.ant.design/docs/introduce/zh</td><td>Angular/Reat</td></tr>
<tr><td>Antv</td><td>蚂蚁金服全新一代数据可视化解决方案，致力于提供一套简单方便、专业可靠、无限可能的数据可视化最佳实践。包含G2、G6、F2、gallery的JS库</td><td>官网：https://antv.alipay.com/zh-cn/index.html<br/>API：https://antv.alipay.com/zh-cn/g2/3.x/api/index.html<br/></td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>Viser</td><td>一个基于 G2 实现的，为数据可视化工程师量身定制的工具</td><td>Github Pages：https://viserjs.github.io/docs.html#/guide/usage</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>Onsen UI</td><td><br/>混合移动应用程序UI组件</td><td>Angular：https://onsen.io/v2/api/angular2/</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>PrimeNG</td><td>很完整的Angular UI组件库</td><td>官网：https://www.primefaces.org/primeng/#/</td><td>Angular</td></tr>
<tr><td>Semantic UI</td><td>适应手机、平板、PC的UI框架</td><td>官网：https://semantic-ui.com/<br/>Angular组件库：https://github.com/vladotesanovic/ngSemantic</td><td>Angular</td></tr>
<tr><td>Admin LTE</td><td>企业级后台UI框架</td><td>官网：https://adminlte.io/<br/>Demo：https://adminlte.io/themes/AdminLTE/index2.html</td><td> </td></tr>
<tr><td>vaadin</td><td>最初是基于Java的Web应用组件和工具</td><td>官网：https://vaadin.com/<br/>Angular：https://vaadin.com/start/v10-angular<br/>Github Pages：https://github.com/vaadin/base-starter-angular</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>Wijmo</td><td>丰富的UI 界面、表格设计、数据处理<br/>Angular组件是纯typescript实现，无依赖</td><td>官网：http://cn.grapecity.com/<br/>Angular：https://www.grapecity.com.cn/developer/wijmojs/angular</td><td>Angular/Reat/Vue.js</td></tr>
<tr><td>blur-admin</td><td>后台UI框架</td><td>Github Pages：https://akveo.github.io/blur-admin/</td><td>AngularJs</td></tr>
<tr><td>Jigsaw(七巧板)</td><td>中兴 Angular UI组件库</td><td>源码: https://github.com/rdkmaster/jigsaw</td><td>Angular</td></tr>
<tr><td>WeUI</td><td>WeUI 是一套同微信原生视觉体验一致的基础样式库，由微信官方设计团队为微信内网页和微信小程序量身设计，令用户的使用感知更加统一。</td><td>官网：https://weui.io/<br/>Angular：https://cipchk.github.io/ngx-weui/#/start</td><td> </td></tr>
<tr><td>Mobile Angular UI</td><td>【移动端】UI框架，基于Boostrap和angularjs实现</td><td>官网：http://mobileangularui.com/<br/>Demo：http://mobileangularui.com/demo/#/</td><td>AngularJs</td></tr>
<tr><td>Ionic</td><td>【移动端】跨平台的移动App开发工具和框架</td><td>官网：https://blog.ionicframework.com/announcing-ionic-cli-v3/</td><td> </td></tr>
<tr><td>mint-ui</td><td>【移动端】基于Vue.js组件库，来自饿了么</td><td>Github Pages：http://mint-ui.github.io/</td><td>Vue.js</td></tr>
</table>

</body>
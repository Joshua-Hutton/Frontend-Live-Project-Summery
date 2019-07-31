# Frontend-Live-Project-Summery
Frontend C# sprint. 

   This was my third sprint of the boot camp and took place immediately after my first C# stand up. During this two week stand up I participated in all the daily stand up as was as a retrospective at the end of each week to discuss what could be improved as a team. The project I worked on was the Management portal project I had been working on the week prior. 
    For this sprint I was to keep my focus on stories that were front end work as much as the available stories would allow without being ideal throughout the sprint. 

My first story was to replace the title in the banner at the top of each page of the website that was hedder text that simply read “Management Portal” with an image of a logo created for the site. 

Changes I made to shared _Layout.chtml partial view. There was code not mine both above and below. 
```c#
<header class="card">
       <img id="site-header">
       <div class="card-img-overlay">
           <a id="header-title" href="@Url.Action("Index", "Home")"><img src="~/Content/images/LOGO_color-Black.png" alt=""/></a>
       </div>
``` 
Css code added to site.css file.
```css
#site-header {
   background-image: url(images/constructionBanner.jpg);
   background-repeat: no-repeat;
   background-size: cover;
   background-position: right;
   width: auto;
   height: 120px;
}
/***this code was modified by me but not wholly mine***/
#header-title {
   text-align: left;
   font-family: 'Vollkorn SC', cursive;
   font-size: 2.7vw;
   color: black;
}
/***********************************************/

#header-title img {
   width: auto;
   Height:75px;
```
The next two story I worked on were the same just in different areas of the site. The first was to change the style on the index of the company news app where all the active jobs were listed from the database. The next was to apply the same styling to the jobs index. The overall look was dictated to me I just had to write the code to achieve the desired effect. Since the look and general layout was the same these stories utilize the same css.

The company news index page. Here I added the Index Body class div tag as well as the row div and column class to get the correct spacing that would move dynamically as the page was resized. The rest of the code already existed. On the jobs index Ill I did was add a div tag with class IndexBody to apply the css the space on that page did not need adjustment. 
```c#
@model IEnumerable<ManagementPortal.Models.CompanyNews>

@{
    ViewBag.Title = "Index";
    Layout = "~/Views/Shared/_Layout.cshtml";
}
<div class="IndexBody">
    <h2 class="text-center">Index</h2>

    <p>
        @Html.ActionLink("Create New", "Create")
    </p>
    <div class="row no-gutters">
    <table class="table">
        <tr>
            <th class="col-1">
                @Html.DisplayNameFor(model => model.Title)
            </th>
            <th class="col-6">
                @Html.DisplayNameFor(model => model.NewsItem)
            </th>
            <th class="col-1">
                @Html.DisplayNameFor(model => model.ExpirationDate)
            </th>
            <th class="col-1"></th>
        </tr>

    @foreach (var item in Model) {
        <tr>
            <td class="col-1">
                @Html.DisplayFor(modelItem => item.Title)
            </td>
            <td class="col-6">
                @Html.DisplayFor(modelItem => item.NewsItem)
            </td>
            <td class="col-1">
                @Convert.ToDateTime(item.ExpirationDate).ToString("MM-dd-yyyy")
            </td>
            <td class="col-1">
                @Html.ActionLink("Edit", "Edit", new { id=item.NewsId }) |
                @Html.ActionLink("Details", "Details", new { id=item.NewsId }) |
                @Html.ActionLink("Delete", "Delete", new { id=item.NewsId })
            </td>
        </tr>
    }

    </table>
    </div>
</div>
```
Css I added to the site.css file. 
```css
/****Styling for Company News Index****/
.newsBody {
background-color: rgba(255, 255, 255,0.8);
padding:10px;
}
.newsBody row{
margin: 10px;
}
```

The last story I worked on for this sprint was the debug why the logout link on the nav bar. When I started the logout link did nothing and the accompanying greeting with the user’s name was not displaying. Not being sure as to how this was supposed to work. I spent the majority of the day researching the issues and trying different fixes until I found an answer. The changes are not profound but that problem solving was quite rewording. 

The original _LoginPartail.chtml file. 
```c#
@using Microsoft.AspNet.Identity
@if (Request.IsAuthenticated)
{
   using (Html.BeginForm("LogOff", "Account", FormMethod.Post, new { id = "logoutForm", @class = "navbar-right" }))
   {
   @Html.AntiForgeryToken()

   <ul class="nav navbar-nav navbar-right">
       <li>
           @Html.ActionLink("Hello " + User.Identity.GetUserName() + "!", "Index", "Manage", routeValues: null, htmlAttributes: new { title = "Manage" })
       </li>
       <li><a href="javascript:document.getElementById('logoutForm').submit()">Log off</a></li>
   </ul>
   }
}
else
{
   <ul class="nav navbar-nav navbar-right">
       <li class="nav-item">@Html.ActionLink("Register", "Register", "Account", routeValues: null, htmlAttributes: new { id = "registerLink", @class = "nav-link" })</li>
       <li class="nav-item">@Html.ActionLink("Log in", "Login", "Account", routeValues: null, htmlAttributes: new { id = "loginLink", @class = "nav-link" })</li>
   </ul>
}
```
And my modified working version. 
```c#
@using Microsoft.AspNet.Identity
@if (Request.IsAuthenticated)
{
  
   <ul>
       <li>
           @Html.ActionLink("Hello " + User.Identity.GetUserName() + "!", "Index", "Manage", routeValues: null, htmlAttributes: new { title = "Manage" })
       </li>
   @using (Html.BeginForm("LogOff", "Account", FormMethod.Post, new { id = "logoutForm", @class = "navbar-right" }))
   {

   @Html.AntiForgeryToken()

       <li>
           <a href="javascript:document.getElementById('logoutForm').submit()">Log off</a>
         
       </li>
   }
   </ul>
  
}
else
{
   <ul>
       <li class="nav-item">@Html.ActionLink("Log in", "Login", "Account", routeValues: null, htmlAttributes: new { id = "loginLink", @class = "nav-link" })</li>
       <li class="nav-item">@Html.ActionLink("Register", "Register", "Account", routeValues: null, htmlAttributes: new { id = "registerLink", @class = "nav-link" })</li>
   </ul>
}

}
```

In addition to these changes there were hard coded action links in the site layout file that I removed and called the _LoginPartail.chtml partial view in their stead. 

There were a few other stories that I worked on during this sprint that I did not include due to there simplicity. Most just called for the changing of a few values to resize certain elements like the nav bar. 


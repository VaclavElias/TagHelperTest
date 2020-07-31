# TagHelperTest

Testing nested partial and child content in partial views.

Changes in aspnetcore/src/Mvc/Mvc.TagHelpers/src/PartialTagHelper.cs

Version 1 - Only 3 lines changed

https://github.com/VaclavElias/aspnetcore/commit/e36395dc81d0307bffb98d5742701f3e1b77fc92

Version 2 - Added RenderTo attribute

https://github.com/VaclavElias/aspnetcore/commit/2563ab361d2f01d57edddb84c8a270fab4cd0c7a

## Index.chsmtl

```razor
<div class="text-center">
    <h1 class="display-4 mb-5 mt-5">Welcome</h1>
    <partial name="_WrapperPartial" model="@(("ASP.NET Documentation", "odd"))">

        <partial name="_HeaderPartial">
            Learn to use ASP.NET Core to create web apps and services that are fast, secure, cross-platform, and cloud-based. Browse tutorials, sample code, fundamentals, API reference and more.
        </partial>

        <partial name="_CardPartial" model="@("Create an ASP.NET Core app in 5 minutes")">
            <p>Ut fusce varius nisl ac ipsum gravida vel pretium tellus tincidunt integer eu augue augue nunc elit dolor, luctus placerat.</p>
        </partial>

        <partial name="_CardPartial" model="@("ASP.NET Core overview")">
            <p>Ut fusce varius nisl ac ipsum gravida vel pretium tellus tincidunt integer eu augue augue nunc elit dolor, luctus placerat.</p>
        </partial>

        <partial name="_CardPartial" model="@("Download .NET")">
            <p>Ut fusce varius nisl ac ipsum gravida vel pretium tellus tincidunt integer eu augue augue nunc elit dolor, luctus placerat.</p>
        </partial>

    </partial>

    <partial name="_WrapperPartial" model="@(("Develop ASP.NET Core apps", "even"))">

        <partial name="_HeaderPartial">
            Choose interactive web apps, web API, MVC-patterned apps, real-time apps, and more.
        </partial>

        <partial name="_CardPartial" model="@("Interactive client-side Blazor apps")">
            <p>Develop with reusable UI components that can take advantage of WebAssembly for near-native performance.</p>
        </partial>

        <partial name="_CardPartial" model="@("RESTful web API apps")">
            <p>Develop RESTful HTTP services with ASP.NET Core web API.</p>
        </partial>

        <partial name="_CardPartial" model="@("Page-focused web UI with Razor Pages")">
            <p>Develop page-focused web apps with a clean separation of concerns.</p>
        </partial>

    </partial>
</div>
```

## _WrapperPartial.cshtml

```razor
@model (string Title, string Section)
<section class="pt-4 pb-4 @Model.Section">
    <div class="container">
        <div class="row">
            <div class="col-md-12 text-center">
                <h2>@Model.Title</h2>
                <div class="row">
                    @ViewData["RenderChild"]
                </div>
                <footer class="mt-4">Section Footer</footer>
            </div>
        </div>
    </div>
</section>
```

## _HeaderPartial.cshtml

```razor
<div class="col-12">
    <p class="lead mb-5 mt-4">
        @ViewData["RenderChild"]
    </p>
</div>
```

## _CaraPartial.cshmtl

```razor
@model string
<div class="col-sm-4">
    <div class="card">
        <div class="card-body">
            @*I want to wrap this <h5 class="card-title">@Model</h5>*@
            @*This is not going to work because of RenderChild name conflict <partial name="_Title">Hello</partial> *@
            @*This is going to work because of render-to*@
            <partial name="_Title" render-to="TitleChild">@Model</partial>
            @ViewData["RenderChild"]
        </div>
    </div>
</div>
```

## _Title.cshmtl

```razor
<h5 class="card-title">@ViewData["TitleChild"]</h5>
```

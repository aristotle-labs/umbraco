###Changes to umbraco forms to allow scripts to load at the bottom of the <body>

After installing the umbraco forms package. Two new files will be present in your site files that you may need to update
- ~/Views/MacroPartials/RenderUmbracoFormScripts.cshtml
- ~/Views/partials/forms/script.cshtml

Taken from: https://our.umbraco.org/Documentation/Products/UmbracoForms/Developer/Rendering-Scripts/ On the InsertUmbracoForm file here we'll make a small change, in the RenderAction call we'll provide an additional argument mode = "form", so go from `Html.RenderAction("Render", "UmbracoForms", new {formId = g});` to `Html.RenderAction("Render", "UmbracoForms", new {formId = g, mode = "form"});`

Then place your Rendor Form Scripts at the bottom of your template page, such as your master.cshtml `@Umbraco.RenderMacro("FormsRenderScripts")`

If their are errors being thrown when you visit the page with the form on it, you might have to change a line in ~/Views/partials/forms/script.cshtml

change the double quotes around the value parameter to single quotes like below, change 
`<input type="hidden" id="values_@Model.FormClientId" value="@Html.Raw(Newtonsoft.Json.JsonConvert.SerializeObject(Model.Pages.SelectMany(p => p.Fieldsets).SelectMany(fs => fs.Containers).SelectMany(c => c.Fields).ToDictionary(f => f.Id, f => f.Value)))" />` to `<input type="hidden" id="values_@Model.FormClientId" value='@Html.Raw(Newtonsoft.Json.JsonConvert.SerializeObject(Model.Pages.SelectMany(p => p.Fieldsets).SelectMany(fs => fs.Containers).SelectMany(c => c.Fields).ToDictionary(f => f.Id, f => f.Value)))' />`

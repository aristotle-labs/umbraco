###How to AJAX a PartialView
In the case where you want to AJAX a simple partial view to save on TTFB you can do this simple trick

Create a Surface Controller in the Controllers Folder, something like this. I already had a partial view called MainPageEvents, that was pulling in 3 featured events on the page.
```
namespace ProjectName.Controllers
{
    public class MainPageFeedCallsController : SurfaceController
    {

        [HttpGet]
        public PartialViewResult GetEventsFeed()
        {
            return PartialView("MainPageEvents");
        }

    }
}
```

Then in your javascript file all you have to do to call it is 
```
$.ajax({
      url: '/Umbraco/Surface/MainPageFeedCalls/GetEventsFeed/',
      type: 'GET',
      dataType: 'html',
      contentType: 'application/json; charset=utf-8',
      success: function (data) {

          // here grab the container that you want to load the data into
          $('.coewrapper').html(data);
      },
      error: function (data) {
          console.info(data);
      }
  });
  ```

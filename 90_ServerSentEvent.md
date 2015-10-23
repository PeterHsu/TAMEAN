# ServerSentEvent範例
透過HTML5的新機制來推播訊息到Browser,是Server->Client單向的訊息傳遞
# html
```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
<div id="divMsg"></div>
<script type="text/javascript">
    var es = new EventSource("Handler1.ashx");
    var stat;

    es.onerror = function (e)
    {
        switch (e.target.readyState) {
            case EventSource.CONNECTING:
                stat = "等待重新連線";
                break;
            case EventSource.CLOSED:
                stat = "連線失敗，停止連線";
                break;
        }
        console.log(stat);
        document.getElementById("divMsg").innerHTML += stat + "<br/>";
    }

    es.onmessage = function (e) {
        console.log(e.data.toString());
        document.getElementById("divMsg").innerHTML += "現在時刻：" + e.data.toString() + "<br/>";
    }

    es.onopen = function (e)
    {
        switch (e.target.readyState)
        {
            case EventSource.CONNECTING:
                stat = "Connecting";
                break;
            case EventSource.OPEN:
                stat = "Open";
                break;
            case EventSource.CLOSED:
                stat = "Closed";
                break;
            default:
                stat = "n/a";
                break;
        }
        document.getElementById("divMsg").innerHTML += "連線狀態：" + stat + "<br/>"
    }

//    es.addEventListener('message', function (e) {

//    }, false);
    </script>
</body>
</html>

```
# Handler.ashx.cs
```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;

namespace ServerSentEvent
{
    /// <summary>
    ///Handler1 的摘要描述
    /// </summary>
    public class Handler1 : IHttpHandler
    {

        public void ProcessRequest(HttpContext context)
        {
            context.Response.ContentType = "text/event-stream";
            context.Response.Write(string.Format("id:{0}\n", 1));
            context.Response.Write(string.Format("data:{0}\n\n", DateTime.Now.ToString()));
            context.Response.End();
        }

        public bool IsReusable
        {
            get
            {
                return false;
            }
        }
    }
}
```

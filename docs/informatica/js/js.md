# JavaScript

## Async functions with Ajax HTTP request

```JavaScript
// Request functions must be async
async function getLastScoringUpdate(){
  
  var response = await $.ajax({
    url: '/maps/last_scoring_update',
    contentType: 'application/json',
    // more settings
  });
  
  // Inside this function, the code will stop till the response is given

  console.log(response.last_update);
  $("#map_last_update").text("Última actualización: " + response.last_update);

  return await response.last_update
}

// When calling it, the code outside won't stop, but can catch actions when response given with .then()
getLastScoringUpdate().then(fecha => initDatePicker(new Date(fecha), new Date(fecha)))

// Code here may be executed before getting a response


```

## Mostrar elemento que ya está en "hidden"=true

```javascript
 $("#id-del-div").attr("hidden", false);

```

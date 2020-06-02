### JavaScript

1. 자바스크립트에서 스프링(자바)로 객체 배열 보내기. (ModelAttribute 파라미터 객체를 List타입으로 받기)

   동적으로 form을 생성하여 보낸다고 가정하자.
   나는 여러가지 필드들과 함께 다음과 같이 생긴 객체 배열을 보내고 싶다.

   ```java
   prices = [
       {
           count : int,
           productPriceId : int
       },
       {
           count : int,
           productPriceId : int
       }, 
       ...
   ]
   ```

   <br>이것을 수행하기 위해 'var prices = []'와 같이 배열을 생성해서 객체를 하나하나 push해 담아 보내도 보고, ModelAttribute가 아니라 일반 RequestParam으로도 보내는 등 오랜 시간 동안 다양한 방법을 시도해보았다.  그러나 도저히 동작하지를 않아서 끈질기게 검색한 끝에 배열을 보내는 법을 알아냈다. 정확히는 배열을 보낸다기 보다 DTO(VO)가 가지고 있는 List의 index 번째에 값을 집어넣도록 이름을 설정하는 것이었다. 다음 코드들을 참고하여 적용해보자.

   <br>js

   ```javascript
   var qtys = document.querySelectorAll(".qty");
   
   qtys.forEach(function(qty, index) {
     var count = qty.querySelector(".count_control_input").value;
     if (count != 0) {
       var productPriceId = json.productPrices[index].productPriceId;
       var hiddenFieldCount = document.createElement("input");
       hiddenFieldCount.setAttribute("type", "hidden");
       hiddenFieldCount.setAttribute("name", "reserveItemPrices[" + index + "].count");
       hiddenFieldCount.setAttribute("value", Number(count));
       form.appendChild(hiddenFieldCount);
   
       var hiddenFieldProductPriceId = document.createElement("input");
       hiddenFieldProductPriceId.setAttribute("type", "hidden");
       hiddenFieldProductPriceId.setAttribute("name", 
              "reserveItemPrices[" + index + "].productPriceId");
       hiddenFieldProductPriceId.setAttribute("value", productPriceId);
       form.appendChild(hiddenFieldProductPriceId);
     }
   })
   ```

   <br>

   controller

   ```java
   @PostMapping(path = "/api/reservations")
   public ReserveItem reservation(
       @ModelAttribute ReserveItem reserveItem, //여기서 자동으로 넣어줌.
       @RequestParam(name="reservationYearMonthDay", required=true) 
       String reservationYearMonthDay) {
     reserveItem.setReservationDate(reservationYearMonthDay);
     reserveItem = reservationManagementService.reserveAnItem(reserveItem, reserveItem.getReserveItemPrices());
     return reserveItem;
   }
   ```

   








  * DIscount amount
    * First example
      * Subtotal of the items: 100
      * Subtotal of the items promo can applicable to: 30
      * Promo Discount: 40
      * I split the 2 amount to
        * 70
          * I will calculate tax and fees from this amount
        * 30
          * 30 <= 40 so the result is 0
    * Second example
      * Subtotal of the items: 100
      * Subtotal of the items promo can be applicable to: 30
      * Promo discount: 15
      * I split the amount to
        * 70
          * I will calculate tax and fees from this amount
        * 30
          * I will subtract 30 - 15 = 15
          * And calculate fee and tax from this amount
        * I will sum the 15 and it's taxes and fees + 70 and it's taxes and fees
  * Discount percentage
    * First example
      * Subtotal of the items: 100
      * Subtotal of the items promo can applicable to: 30
      * Promo Discount Percentage: 
      * I split the 2 amount to
        * 70
          * I will calculate tax and fees from this amount
        * 30
          * I will calculate the tax and fees from 30 and then apply 100% discount to this calculated number
          * So discount is slightly higher than 30, it is 30 + its fee and taxes
    * Second example
      * Subtotal of the items: 100
      * Subtotal of the items promo can be applicable to: 30
      * Promo discount percentage: 50%
      * I split the amount to
        * 70
          * I will calculate tax and fees from this amount
        * 30
          * I will calculate tax and fee from 30
          * apply 50% discount to the 30 + its taxes and fees
        * I will sum the result of 30 calculation + 70 and it's taxes and fees
  * When calculating Free delivery - I will just set promo discount as Delivery cost, tax and fees from subtotal is calculated from subtotal as usual
  * If we are calculating with Buy X and Get Y or get X for FREE I will always subtract the cost of the items from the subtotal and then calculate tax and fees
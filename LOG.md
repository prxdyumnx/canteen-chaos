# Debug log

Your notes. One entry per bug you fixed, using the template below.

This file is read as carefully as your code. A correct fix you cannot
explain counts for little; a bug you could not fix but investigated
honestly still counts for something.




### CC-01 — "The search suggestions are behind everything"

**Reproduced:** When we type dish name in search bar , the suggestions appear behind other page elements , and only top part could be clicked.

**Cause:** The .search-wrap element had z-index 1 whereas category bar has z-index 40 , that's why search suggestions are behind category bar 

**Fix:** Increased z-index of .search-wrap in frontend/style.css from 1 to 69 so that search-wrap element appear in front of category bar 

**Checked:** verified that search suggestions appear above category bar and is fully functional and can be clicked.

**Time:** 10-15 minutes

### CC-02 — "Can't read anything in dark mode"

**Reproduced:** When we switch the website to dark mode , dishes name and prices became difficult to read because their text colour became ink colour against dark background.

**Cause:** In frontend/style.css , the .dish-body used text colour ink(#2b2118) . This colour doesn't change even when we change our theme to dark mode . The project already defined variable --ink , in that variable it is already defined to change text colour according to theme , but .dish-body was not using it.

**Fix:** Replaced colour (color: #2b2118 ) with (color: var(--ink)) in the dish-body in frontend/style.css. This allows text color to change according to theme .

**Checked:** Verified dish name and price in both light and dark mode , text is readable and doesn't affect other elements.

**Time:** 15 minutes 

### CC-03 — "The menu is wider than my phone"

**Reproduced:** When we test menu at different screen widths , we found that below 625px, the menu layout become too wide and content on upper right part screen get cutoff.

**Cause:** Menu grid was not adapting properly to narrow screen width, multiple dishes were displayed on smaller screen in one row caused this layout issue.

**Fix:** Added CSS media query in frontend/style.css for screens with maximum width of 625px. In this query we changed(.menu-grid layout )to single column usig( grid-template-columns: repeat(1, 1fr);) . This will make the dishes stack vertically one by one on each other .

**Checked:** Tested the menu at different pixels and it worked fine.

**Time:** 35 minutes 

### CC-04 — "The buttons are visible but taps are not working"

**Reproduced:** When viewing menu on tablet sized screen , add to cart and favourite button was visible but tapping on them didn't work.

**Cause:** The (.dish-card::after) and (.img-wrap::after pseudo-elements) created overlays which hinders clicking.

**Fix:** Added pointer-events:none; this prevents elements to hinder the underlying interactive elements and we can reach underlying elements that is add to cart and favourite button 

**Checked:** Test the add to cart and favourite buttons in tab mode and it worked perfectly.

**Time:** 2-3 hours

### CC-06 — "I ordered more than they had"

**Reproduced:** When only 2 samosas were in stock ,we can order more than 2 samosas.

**Cause:** Validation only checked if item is zero it cannot be ordered , it did not compare available stock with with user request and we can order as many item we can.

**Fix:** Changed the condition from (qty> MAX_QTY_PER_DISH) to (qty> Number(dish.stock)) in backend/logic/validation.js to reject order when request exceeds available stock.

**Checked:** Now 5 samosas can't be ordered as stock is only of 2.

**Time:** 1 hour


### CC-07 — "Cancelled orders do not restore the correct stock quantity"

**Reproduced:** when we cancel order , stock quantity decreased instead of staying same as before.

**Cause:** Stock update logic used subtraction instead of addition when we cancel an order, that is why stock is reduced despite being cancelled 

**Fix:** Changed stock update operation from dish.stock - line.qty to dish.stock + line.qty in releasestock() , ensuring that cancelled order's quantity in restored.

**Checked:** Now when we cancel an order , full stock is restored.

**Time:** 30 minutes 

### CC-08 — "Expired coupons are still accepted"

**Reproduced:** When we use FRESHERS24 even though it is expired , we can still get discount

**Cause:** Coupon validation function did not check whether coupon expiry date has passed or not. Although expired coupon were filtered out from available coupon list , but still validation function can accept an expired coupon when typed directly

**Fix:** Added check manually using !Number.isFinite(expires.getTime()) || expires < to reject invalid expiry dates and expired coupons and display message ' This coupon has expired '

**Checked:** FRESHERS24 doesn't work now.

**Time:** Most of the day spent finding this bug.

### CC-10 — "Price sorting displays dishes in the wrong order"

**Reproduced:** When we select show dishes by price from high to low , it shows from low to high and vice versa.

**Cause:** The comparision logic for ascending and descending price sorting was reversed.

**Fix:** Corrected sorting logic in backend/logic/search.js by using a.price - b.price for low-to-high sorting and b.price - a.price for high-to-low sorting.

**Checked:** Tested both sorting options and verified that dishes appear in correct order.

**Time:** 20 minutes


## CC-0X — "<the complaint, in short>"

**Reproduced:**

**Cause:**

**Fix:**

**Checked:**

**Time:**



## Could not fix

For anything you investigated but did not solve. Say what you tried and
where you got to. This is worth marks — leaving it blank when you got
stuck is not.

### CC-0X — "<the complaint>"

**What I tried:**

**Where I got to:**

**What I would try next:**



## Extra credit

Anything not on the bug log: a problem you found yourself, a test you
wrote, or a fix you are unsure about. Same format, plus one line on how
you noticed it.

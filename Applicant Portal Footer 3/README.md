
# JavaScript Function Description

Information for upkeep and debugging of Applicant Portal scripts

#### Due to PeopleAdmin's portal management setup, there is no explicit location for JavaScript to be implemented in the site. For this reason an HTML element located closer to the bottom of the page was chosen. 

Below you will find documentation regarding each of the JavaScript functions. Each time a function is added, refactored, or removed should result in this documentation being rewritten to some degree.


## Functions

### positionFooter()

The positionFooter() function is used to force the footer to the bottom of the screen on the Job Alerts page. On all pages that need to force the Footer to the bottom of the page, the padding of the Nav Bar is extended to the top of where the Footer should be placed. Job Alerts is one of the few pages that can be visited while either logged out or in where the Footer is not already at the bottom of the page.

The Function Call only executes on the Job Alerts page, which is checked in the first condition above the function call `if (document.getElementById("interest_cards_index") && `. The second condition `window.screen.width >= 1200)` causes the footer function to not be called in mobile resolution.

The function's first priority is to determine if the user is logged in or not. This is done by checking the Nav Bar and counting the number of elements contained within. If the number of NavLink elements is less than 8, the user is not logged in. 

`if (document.getElementById("navLinks").children.length < 8)` checks the number of child elements. The difference in spacing comes into play between users on FireFox or Chrome, so the second check ` if (typeof InstallTrigger !== "undefined")` is considered true if the page is viewed on a FireFox browser.

Extending the Padding:

The function then selects the Nav Bar and accesses its Padding Bottom property with `document.getElementById("nav").style.paddingBottom` and assigns a value of 23.7em for logged in FireFox, 23.6em for logged in Chrome, or 11.8em for a logged out state.



### alterButtonStyle()

PeopleAdmin's default styling had the classes for the Account Settings and Demographic Information's Submit Button set differently, which was noticable and inconsistent. This function simply capiitalizes the U in Update for the button label and changes the class name of the element so the CSS rules can be properly assigned.

The conditional above the function call will result in true if the user is on the Edit Account Settings page. `if (document.getElementById("users_edit"))`.

Within the function a named constant, button, is declared and assigned the value of `document.getElementsByName("commit")[0]`. PeopleAdmin did not give this button an id property, so it must be accessed through a list of Node Objects. Fortunately there is only one element with the name commit on the page, so index 0 will work each time. If the value stored within the chosen variable isn't undefined, the class name of button is updated to `"btn"` to apply the CSS rules for that class using `button.className = "btn"`. The label of the button is updated to "Update" using `button.value = "Update"`.

### updateApplyButton()

For the Responsive Mobile View of the site, the Apply to this Job button on the Job Description page is noticably thinner than the other two buttons. The button exists as two different HTML elements depending if the user is logged in or not, so this function will identify which element exists and modify that one accordingly.

The conditional above the function call contains two statements. The first, `if (document.getElementById("postings_show") && `, results in true if the user is on the job description page. The second, `window.screen.width <= 768)`, only results in true on mobile resolutions.

Within the function a variable is declared for the element to be updated. When logged in the element is a Form, when logged out the element is an A Tag. The variable is named form in this instance. Next is a conditional to identify which button exists. Neither element has an id property, so the conditional checks for the class name. `if (document.getElementsByClassName("apply-to-job-form").length !== 0)` checks if there are any elements on the page with that name, which is the element that exists if a user is logged in. If this returns true, that form element is assigned to the form variable with `form = document.getElementsByClassName("apply-to-job-form")[0]`. If that returns false another conditional is checked, `if (document.getElementsByClassName("secondary_button_color").length !== 0)`, which checks for any elements that exist if the user is not logged in. If this results in true then the form variable is updated to `form = document.getElementsByClassName("secondary_button_color")[0]`. Finally, if form variable is not undefined (`if (form !== undefined)`), meaning that one of those if statements resulted in true, the width property is modified with `form.style.width = "15em"`

#### PeopleAdmin JavaScript Function Documentation
#### - Matthew Greco 1/30/2024

Prezi Signup Form Bug Report.md

#Summary

Since the signup form is the first true interaction with the Prezi brand, I believe this small CSS/HTML bug would be worthwhile to fix. It is a low-cost high-reward bugfix.

The **[signup page](https://prezi.com/profile/registration/?license_type=PUBLIC) for Prezi** has some alignment issues when resizing the browser window. The First and Last name fields are misaligned between the full width and mobile width. The 'Signup with LinkedIn' and 'Signup with Facebook' buttons do not resize correctly with their containing box and therefore stick out between full width and mobile width.

![Screen shot of Prezi signup form bug](Prezi_SignupPage_Bug.jpg)

![Screen shot of Prezi signup form bug](Prezi_SignupPage_Bug2.jpg)

#Screen cast

###Scenario 1: on Chrome 34 and Firefox 29
http://youtu.be/JQraY4xBh20

###Scenario 2: on IE 8
Decided not to record screen cast as the whole page is not responsive to changing browser width.

#Recommended solution

1) First name and Last Name input fields

The problem is with browser size between 765pm and 940px. Below and above the form looks OK. There are at least two ways to fix this issue.

The first method involves fixing the input.span4 class in @media (max-width: 940px) and (min-width: 765px) so that each would take up max 50% of the available width. This, however could produce very tiny input fields that could create an uncomfortable UX.

The second method is to get rid of the special formatting for the first and last name fields and use the same wrappers as all the other input fields. In this case we would remove from the DOM the element holding both first and last names, and instead have two child nodes each containing only one field. The corrected HTML would look like this:

```html
<li class="control-group">
	<input name="first_name" type="text" 
	placeholder="First name" class="input-large span8 textfield" 
	id="id_first_name">
</li>

<li class="control-group">
	<input name="last_name" type="text" 
	placeholder="Last name" class="input-large span8 textfield" 
	id="id_last_name">
</li>
```

2) social signup
- remove: `.well .btn { width: 238px; }` // solves the problem, as buttons will not protrude outside of containing element
- remove: `.btn { height: 26px; }` // allows the button to include two lines of text when text button is wrapped
- add: `.well .btn { display: block; }` // otherwise buttons will be positioned next to each other in mobile view

Hope this helps.

Monthy

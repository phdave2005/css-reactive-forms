# CSS Reactive Forms
CSS Reactive Forms seeks to emulate a "reactive forms" UX without ANY Javascript, with the understanding that this experience may NOT ever be able to fully close the gap relative to what a Javascript-based reactive forms UX can deliver. However, as CSS becomes more sophisticated, it is believed this gap will diminish.

# Introduction
&nbsp;&nbsp;&nbsp;&nbsp;[Reactive Forms](https://angular.dev/guide/forms/reactive-forms/) is a user experience (UX) paradigm which uses a scripting language (most notably Javascript) to track changes in form state, and subsequently deliver cues to the user about these changes. The scope of these cues include, but are not limited to, field/field-group/form validity, accessibility control, and layout changes. As the differences between these form states is controlled by logical gates, implementation of this UX via Javascript, and more relevantly, frameworks such as Angular, has been for over a decade the "expected" implementation.<br>
&nbsp;&nbsp;&nbsp;&nbsp;However, a Javascript-based implementation does have certain disadvantages, even if one ignores performance-based issues that are associated with Javascript (which can be debated). One of the most significant disadvantages is that Javascript usage can be subject to security vulnerabilities. As companies increasing turn to code-scanning tools such as Fortify and SonarQube, these vulnerabilies not only become more easily detected, but also, can become blockers to development. Since CSS is much less vulnerable to security vulnerabilities, a "Javascript-free" approach to UX enhancement becomes more valuable.<br>
&nbsp;&nbsp;&nbsp;&nbsp;The purpose of **CSS Reactive Forms** is to demonstrate one example of this approach, delivering a "reactive-forms-like" UX that, though less powerful than what a Javascript-based approach CAN deliver, is anticipated to be an increasingly close facsimile of Javascript-based reactive forms as CSS becomes increasingly sophisticated going forward.<br>

# Documentation
&nbsp;&nbsp;&nbsp;&nbsp;**CSS Reactive Forms** v1.0 delivers its UX largely based on [CSS management of state](https://drafts.csswg.org/selectors/) made possible by the
     
- input pseudoclasses such as **:checked**, **:user-invalid**, **:user-valid**, and **:placeholder-shown**
- relational pseudoclass **:has()**
- user-action pseudoclasses **:focus** and **:focus-within**

in combinations with native HTML5 validations made possible by input types email, url, etc, and their associated attributes such as **minlength** or **required**.

&nbsp;&nbsp;&nbsp;&nbsp;The attainment of certain form states can be mimicked by CSS. For example, the submit button of a &lt;form&gt; can be held in a "disabled-like" state (similar to reactive forms) by application of declarations such as `pointer-events: none` and an `opacity: 0.5`, etc., provided that the &lt;form&gt; **:has(:user-invalid)** for at least 1 field. Another example would be to mimic an invalid field of a reactive form by applying a `color: red`, etc. declaration within a rule such as **form :user-invalid**. In **CSS Reactive Forms**, additional form state styling can be activated by adding the class **enhanced-form** to the &lt;form&gt; tag and the class **enhanced** to the &lt;legend&gt; tag; the reason for this optional, 'enhanced' UX is that the additional styles may not fit all use cases. All of the enhanced form styles are scoped within a nested section within the **form** selector: and the class 
```
form {
    .
    .
    .
    &.enhanced-form {
      /* "Enhanced" styles reside in here */
    }
    .
    .
    .
}
```
&nbsp;&nbsp;&nbsp;&nbsp;All of these rules are within the scope of a **form** selector using nested CSS, and styles have been more easily abstracted using CSS &lt;custom-property-names&gt; via application of **var()**. All &lt;custom-property-names&gt; have been moved to the top within the **form** selector to enable an author to more easily tailor styles to a use-case without tampering with any of the underlying declarations, which *could* destroy the styling if applied by an inexperienced author. In fact, the ideal case that will be sought is one in which _all_ use-case-specific adjustments can be made by editing the &lt;custom-property-name&gt; set alone.

# Example 1: Tailoring the invalid field color via &lt;custom-property-name&gt;
```
form {
    .
    .
    .
    --invalid-color: red; /* Changing here applies globally without delving into any declarations */
    .
    .
    .
}
```
instead of
```
form {
    .
    .
    .
    &:user-invalid {
      border: 1px solid var(--invalid-color); /* More risky for an inperienced user to tailor the style here */
    .
    .
    .
}
```
---

# Example 2: Tailoring the invalid form symbol from 'X' to '!' in an 'Enhanced UX'
```
<!-- in HTML template -->
<form class="enhanced-form">...</form>

/* from CSS Reactive Forms */
form {
    .
    .
    .
    --enhanced-form-invalid-symbol: "\0021"; /* Unicode '!' is shown to left; alternatively, plain text "!" would also work */
    .
    .
    .
}
```
---

&nbsp;&nbsp;&nbsp;&nbsp;Disabled fields can be enabled by inputting a controller field with valid data, provided the controller field's parent container has class **disabled-field-controller** and the target disabled field's parent container is in a sibling container that has the class **disabled-field-controller-target** ([subsequent sibling selectors](https://drafts.csswg.org/selectors/#general-sibling-combinators)). For a disabled group of fields, the parent to ALL the controller fields must have class **disabled-group-controller-fields** and the target disabled fields' parent container is in a sibling container that has the class **disabled-field-controller-targets**.<br>
&nbsp;&nbsp;&nbsp;&nbsp;Similarly, the visibility of hidden groups can be toggled by checking/unchecking a controller field (checkbox, radio button, or dropdown option), provided the controller field's parent container has class **hidden-group-controller** and the hidden group's parent container is in a sibling container (relative to the controller) that has the class **hidden-group-controller-target**.


Example forms can be found at JSFiddle:

- https://jsfiddle.net/CSSBurner/3vbk9gwm/
- https://jsfiddle.net/CSSBurner/zrohxcwj/



      

  

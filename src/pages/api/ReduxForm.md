<ol class="breadcrumb">
  <li><a href="#/">Redux Form</a></li>
  <li><a href="#/api">API</a></li>
  <li class="active">`reduxForm(config:Object)`</li>
</ol>

# `reduxForm(config:Object)`

Creates a decorator with which you use `redux-form` to connect your form component to Redux. The keys in the `config`
parameter are as follows.

```javascript
var reduxForm = require('redux-form').reduxForm;  // ES5
```
```javascript
import {reduxForm} from 'redux-form';  // ES6
```

## Config Properties

**IMPORTANT: All of these configuration options may be passed into `reduxForm()` at "design time" or passed in as
props to your component at runtime.**

### Required

#### `fields : Array<String>` [required]

> a list of all your fields in your form.

#### `form : String` [required]

> the name of your form and the key to where your form's state will be mounted under the `redux-form` reducer

### Optional

#### -`asyncBlurFields : Array<String>` [optional]

> field names for which `onBlur` should trigger a call to the `asyncValidate` function. Defaults to `[]`.

> See [Asynchronous Blur Validation Example](#/examples/asynchronous-blur-validation) for more details.

#### `asyncValidate : (values:Object, dispatch:Function) => Promise<undefined, errors:Object>` [optional]

> a function that takes all the form values and the `dispatch` function, and returns a Promise that will resolve if
the validation is passed, or will reject with an object of validation errors in the form
`{ field1: <String>, field2: <String> }`.

> See [Asynchronous Blur Validation Example](#/examples/asynchronous-blur-validation) for more details.

#### `formKey : String` [optional]

> The key for your sub-form.

> See [Multirecord Example](#/examples/multirecord) for more details.

#### `initialValues : Object<String, String>` [optional]

> The values with which to initialize your form in `componentWillMount()`. Particularly useful when
[Editing Multiple Records](#/examples/multirecord), but can also be used with single-record forms. The values 
should be in the form `{ field1: 'value1', field2: 'value2' }`.

#### `onSubmit : Function` [optional]

> The function to call with the form data when the `handleSubmit()` is fired from within the form component. If you
do not specify it as a prop here, you must pass it as a parameter to `handleSubmit()` inside your form component.

> If your `onSubmit` function returns a promise, the `submitting` property will be set to
`true` until the promise has been resolved or rejected. If it is rejected with an object matching
`{ field1: 'error', field2: 'error' }` then the submission errors will be added to each field (to the
`error` prop) just like async validation errors are. If there is an error that is not specific 
to any field, but applicable to the entire form, you may pass that as if it were the error for a field
called `_error`, and it will be given as the `error` prop.

#### `readonly : boolean` [optional]

> if `true`, the decorated component will not be passed any of the `onX` functions as props that will allow 
it to mutate the state. Useful for decorating another component that is not your form, but that needs to know
about the state of your form.

#### `reduxMountPoint : String` [optional]

> The use of this property is highly discouraged, but if you absolutely need to mount your `redux-form` reducer at 
somewhere other than `form` in your Redux state, you will need to specify the key you mounted it under with this 
property. Defaults to `'form'`.

> See [Alternate Mount Point Example](#/examples/alternate-mount-point) for more details.

#### `touchOnBlur : boolean` [optional]

> marks fields as `touched` when the blur action is fired. Defaults to `true`.

#### `touchOnChange : boolean` [optional]

> marks fields as `touched` when the change action is fired. Defaults to `false`.

#### `validate : (values:Object, props:Object) => errors:Object` [optional]

> a synchronous validation function that takes the form values and props passed into your component.
If validation passes, it should return `{}`. If validation fails, it should return the validation errors in the
form `{ field1: <String>, field2: <String> }`. Defaults to `(values, props) => ({})`.

> See [Synchronous Validation Example](#/examples/synchronous-validation) for more details.

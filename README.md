# OpenChair Online Scheduling Widget

Embeddable online scheduling widget built with React.

## Usage

### Installation

Navigate to the source code of a Rooster Grin site that has been onboarded and add the following directly above the closing body tag.

```html
<script
  src="https://onlineschedulingv2.threadcommunication.com"
  type="text/javascript"
></script>
<script type="text/javascript">
  OpenChair.init({
    token: 'superhugetoken',
    option1: 'foo',
    option2: 'bar',
  })
</script>
```

### Authentication

| Property Name        | Type   | Value                                     |
| -------------------- | ------ | ----------------------------------------- |
| token **(required)** | String | The authorization token for your practice |

### Booking Window Configuration

| Property Name           | Type       | Value                                                                                                                |
| ----------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------- |
| bookingsEndOffsetWeeks  | Integer    | The last booking will be this many weeks from 'now'. Note: Must coordinate with backend widget_weeks_window setting. |
| bookingsStartOffsetDays | Integer    | The first booking will be this many days from 'now'.                                                                 |
| customTimeBounds        | [int, int] | Lower and upper bound times for the time dropdown.                                                                   |

### Display Customization

| Property Name          | Type    | Value                                                                                              |
| ---------------------- | ------- | -------------------------------------------------------------------------------------------------- |
| brandName              | String  | This will replace the practice name everywhere it appears in the widget                            |
| locationNameSwap       | Object  | Replace a location name for example {'Delite': 'foo', 'Johns Island': 'bar'}                       |
| customMainButtonLabel  | String  | Customizes the button label on the widget. Default is 'Schedule Consultation'.                     |
| customSubHeaderMessage | String  | Customizes the message shown above 'Choose a date'. Default is 'Schedule an Initial Consultation'. |
| hideMainButton         | Boolean | If true, the main widget button will be hidden                                                     |
| hideTooltipHeader      | Boolean | If true, the main button will not show the number of available appointments in the week            |
| mainButtonLeft         | Boolean | If true, it will open the widget on the left side                                                  |

### Location & Map Settings

| Property Name                | Type    | Value                                                                                                                                                         |
| ---------------------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| disableMap                   | Boolean | This disables the map feature within the widget. The widget will not interfere with other google maps calls.                                                  |
| floatDownLocsWithoutBookings | Boolean | This will place locations with no bookings to the bottom of the locations list. Sorts locations for each selected day.                                        |
| hideLocsWithoutBookings      | Boolean | This will hide locations without any bookings for each selected day.                                                                                          |
| skipDateSelection            | Boolean | Makes widget jump directly from zipCodeSearch to booking selection. **Only works with zipCodeSearch.**                                                        |
| sortPerSpecificLocations     | Boolean | This will sort the locations list by the order of IDs in the `specificLocations` array. Requires `specificLocations` array to determine the order to sort by. |
| specificLocations            | Array   | If you pass an array of location ids in, only those locations an their bookings will be available to end users                                                |
| zipCodeSearch                | Boolean | This will add an input to enter a zipcode to sort practices by distance                                                                                       |

### Patient Form Configuration

| Property Name       | Type             | Value                                                                                                                                                                                                                  |
| ------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| adultPatientsOnly   | Boolean          | If true, hides adult/child toggle and only creates new patients as adults                                                                                                                                              |
| adultPatientsMinAge | Integer          | Ensures adult patient's age is greater than or equal to this number. Shows an error message next to the submit button: "Adult patients {{adultPatientsMinAge}} and over only. Please contact us for details."          |
| extraQuestions      | Array of objects | Adds questions to the patient form. Each object must have `type`. Type `radio` must also have: `question`, `keyname`, `option1`, `option2`, `required`. Type `text` must also have: `question`, `keyname`, `required`. |
| hideZipInput        | Boolean          | Hides zip input on patient form (unrelated to zip search).                                                                                                                                                             |
| minorPatientsOnly   | Boolean          | If true, hides adult/child toggle and only creates new patients as children                                                                                                                                            |
| minorPatientsMaxAge | Integer          | Ensures minor patient's age is less than or equal to this number. Shows an error message next to the submit button: "Minor patients {{minorPatientsMaxAge}} and under only. Please contact us for details."            |
| policyCheckbox      | String           | Add a checkbox to the widget for users to agree to the privacy policy.                                                                                                                                                 |
| phoneNumberRequired | Boolean          | If false, phone number will not be required on the patient form. Default value is true.                                                                                                                                |
| postalCode          | Boolean          | If true, form will display field as "Postal Code" instead of "Zip Code".                                                                                                                                               |
| textAreaLabel       | String           | Lets you customize the text area label. Defaults to "Message".                                                                                                                                                         |
| textAreaRequired    | Boolean          | A value of `true` will make the text area a required field.                                                                                                                                                            |

### Contact & Messages

| Property Name              | Type    | Value                                                                                                                                                                                           |
| -------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contactPhoneNumber         | String  | This will add a phone number to the bottom of the widget container that clients can use to call the practice. Must be formated as all numbers and include the country code. e.g.: `14155551234` |
| hideMessageOnMapRow        | Boolean | This will hide the same message as the contactPhoneNumber (or customMessage) on the bottom of the secondary widget container (MapRow)                                                           |
| showPhoneMessageOnDropdown | Boolean | This will show the same message as the contactPhoneNumber (or customMessage) on the bottom of the initial widget container (dropdown)                                                           |

### Widget Rendering

| Property Name | Type    | Value                                                            |
| ------------- | ------- | ---------------------------------------------------------------- |
| demo          | Boolean | If true, requires query string `?demo=true` to render the widget |

### Anti-Spam Protection

Protect your form submissions from automated spam and ensure genuine patient bookings.

| Property Name    | Type    | Value                                        |
| ---------------- | ------- | -------------------------------------------- |
| recaptchaEnabled | Boolean | adds a recaptcha to the patient form section |

### Redirect

Redirect users after successful form submission. Usually used for conversion tracking. See Google Analytics section below for related info.

| Property Name   | Type    | Value                                                                       |
| --------------- | ------- | --------------------------------------------------------------------------- |
| redirect        | String  | Send the user to a thank you page or elsewhere.                             |
| skipAttribution | Boolean | On successful submit, skip attribution and go straight to the redirect url. |

### Automatically open widget on page load

Clients have the option to default the widget to open on page laod. This is useful if they want to have a direct link to the scheduling widget for Facebook posts and the like.

To do this add the following query parameter to the URL, `schedule_consultation=true`. The full url will look something like this – `https://www.roostergrin.com?schedule_consultation=true`

### Launch Widget from External Element

The widget can be launched from any element on the page. All you have to do is add the class `openchair-widget`, then when that element is clicked, the widget will open.

### Google Analytics

The widget captures several events using Google's global site tag. For data to be sent to a Google Analytics account, it requires the following code to be added to `<head>` of the site on any page where the widget is available with the appropriate measurement ID.

```html
<script
  async
  src="https://www.googletagmanager.com/gtag/js?id=[GOOGLE-MEASUREMENT-ID]"
></script>
<script>
  window.dataLayer = window.dataLayer || []
  function gtag() {
    dataLayer.push(arguments)
  }
  gtag('js', new Date())
  gtag('config', '[GOOGLE-MEASUREMENT-ID]')
</script>
```

The table below describes the events and parameters that are captured.

| Name                  | Description                                                    | Parameters                               |
| --------------------- | -------------------------------------------------------------- | ---------------------------------------- |
| rg_os_opened          | Fires only once when widget is opened.                         |                                          |
| rg_os_appt_selection  | Fires when a user selects date and time for their appointment. | selected_datetime <br> selected_location |
| rg_os_form_successful | Fires when form is successfully sent to backend.               | booked_datetime <br> booked_location     |
| rg_os_form_error      | Fires if there is an error sending form                        | form_error                               |


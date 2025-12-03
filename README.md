# OpenChair Online Scheduling Widget

Embeddable online scheduling widget built with React.

## To Run This App Locally

1. clone the repo

- run `npm install` to install dependencies
- You'll need to make sure roostergrin/rooster-reminders-back-end is running
- run `echo 'API_BASE_URL=http://localhost:3001/api/v1' > .dev.env`
- Create a token for a practice in your database using the `schedule_widgets` API endpoint
- Add the token into the `.dev.env` file as follows `TOKEN=YOUR_NEW_TOKEN`
- Finally run `npm start`
- The widget should now be running on port 8080 showing data for the practice from the token

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

| Property Name       | Type             | Value                                                                                                                                                                                                                                  |
| ------------------- | ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| adultPatientsOnly   | Boolean          | If true, hides adult/child toggle and only creates new patients as adults                                                                                                                                                              |
| adultPatientsMinAge | Integer          | Ensures adult patient's age is greater than or equal to this number. Shows an error message next to the submit button: "Adult patients {{adultPatientsMinAge}} and over only. Please contact us for details."                          |
| extraQuestions      | Array of objects | Adds questions to the patient form. Each object must have `type`. Type `radio` must also have: `question`, `keyname`, `option1`, `option2`, `required`. Types `text` and `checkbox` must also have: `question`, `keyname`, `required`. |
| hideZipInput        | Boolean          | Hides zip input on patient form (unrelated to zip search).                                                                                                                                                                             |
| minorPatientsOnly   | Boolean          | If true, hides adult/child toggle and only creates new patients as children                                                                                                                                                            |
| minorPatientsMaxAge | Integer          | Ensures minor patient's age is less than or equal to this number. Shows an error message next to the submit button: "Minor patients {{minorPatientsMaxAge}} and under only. Please contact us for details."                            |
| minorPatientsMinAge | Integer          | Ensures minor patient's age is greater than or equal to this number. Shows an error message next to the submit button: "Minor patients {{minorPatientsMinAge}} and over only. Please contact us for details."                          |
| policyCheckbox      | String           | Add a checkbox to the widget for users to agree to the privacy policy.                                                                                                                                                                 |
| phoneNumberRequired | Boolean          | If false, phone number will not be required on the patient form. Default value is true.                                                                                                                                                |
| postalCode          | Boolean          | If true, form will display field as "Postal Code" instead of "Zip Code".                                                                                                                                                               |
| textAreaLabel       | String           | Lets you customize the text area label. Defaults to "Message".                                                                                                                                                                         |
| textAreaRequired    | Boolean          | A value of `true` will make the text area a required field.                                                                                                                                                                            |

**hidden option alert**

when you're using filterOptions, we can dynamically set the below depending on which button the user clicks
> adultPatientsOnly, adultPatientsMinAge, minorPatientsOnly, minorPatientsMinAge, minorPatientsMaxAge

if you’d like to do this for any client, plz send the details to fullstack and make sure any 'hardcoded' params are not in the widget script

### Contact & Messages

| Property Name              | Type    | Value                                                                                                                                                                                                             |
| -------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| customMessage              | String  | Adds a message to the bottom of the widget container on the appointment selection screen. Overrides contactPhoneNumber.                                                                                                                         |
| contactPhoneNumber         | String  | Adds a generic message with a clickable phone number to the bottom of the widget container on the appointment selection screen. Must be formatted as all numbers and include the country code. e.g.: `14155551234`. Overridden by customMessage. |
| hideMessageOnMapRow        | Boolean | This will hide the customMessage or contactPhoneNumber message on the appointment selection screen.                                                                                                               |
| showPhoneMessageOnDropdown | Boolean | This will show the customMessage or contactPhoneNumber message on the bottom of the initial widget container.                                                                                                     |

### Widget Rendering

| Property Name | Type    | Value                                                            |
| ------------- | ------- | ---------------------------------------------------------------- |
| demo          | Boolean | If true, requires query string `?demo=true` to render the widget |

### Anti-Spam Protection

Protect your form submissions from automated spam and ensure genuine patient bookings.

| Property Name    | Type    | Value                                        |
| ---------------- | ------- | -------------------------------------------- |
| recaptchaEnabled | Boolean | adds a recaptcha to the patient form section. to be fully effective, fullstack has to update practice.os_recaptcha_enabled in the backend |

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

### Running Development App on a Public URL

To do cross-browser testing on BrowserStack or other devices you can expose your local build on a public URL.

1. Install [localtunnel](https://github.com/localtunnel/localtunnel)

- Expose your backend on a public URL
  - Start up a localtunnel process for the backend port `lt --port 3001`
  - shut down the BE server
  - In `config/application.yml` under development change the BASE_URL to be the localtunnel url you just started
  - restart the server
- Setup the frontend
  - Change the `API_BASE_URL` env variable file
  - Start up a localtunnel process for the frontend port `lt --port 8080`
- Generate a new widget token
  - The endpoint URL should be `LOCAL_TUNNEL_BACKEND_URL/admin/schedule_widgets`
  - You map also need to generate a new authorization token before this will work
  - generate the token using the practice id and localtunnel url for the front-end
  - Take the new token and set the `TOKEN` environment variable in the `.dev.env` file
- Restart the front-end server
  - Use `npm run start:expose`
- Your frontend should now be useable on the front-end localtunnel URL

You should now see your app running on the localtunnel url for the front end app

### Analytics and Tag Manager

The widget now sends events to Google Tag Manager if it's present on the page, without requiring any additional scripts. If `window.dataLayer` exists, events are pushed to it with the `event` name and parameters. If `window.dataLayer` is not present but `gtag` is available, events are sent using `gtag('event', ...)`. If neither is present, the widget safely no-ops.

You do not need to add `gtag` if you're already using Google Tag Manager. If you prefer using the global site tag (gtag.js) without GTM, you can still include it and events will be sent via `gtag`.

The table below describes the events and parameters that are captured.

| Name                          | Description                                                    | Parameters                                      |
| ----------------------------- | -------------------------------------------------------------- | ----------------------------------------------- |
| rg_os_opened                  | Fires only once when widget is opened.                         |                                                 |
| rg_os_find_appointments_click | Fires when user clicks the "Find Appointments" button.         | selected_date <br> selected_time <br> timestamp |
| rg_os_appt_selection          | Fires when a user selects date and time for their appointment. | selected_datetime <br> selected_location        |
| rg_os_form_successful         | Fires when form is successfully sent to backend.               | booked_datetime <br> booked_location            |
| rg_os_form_error              | Fires if there is an error sending form                        | form_error                                      |

#### Consuming events with Google Tag Manager

If your site uses Google Tag Manager, you can listen for all widget events with a single trigger and forward them to GA4 (or any other tool):

1. Create Data Layer Variables

- In GTM → Variables → New → Data Layer Variable, create the following (all default settings):
  - `DLV - selected_date` with Data Layer Variable Name `selected_date`
  - `DLV - selected_time` with Data Layer Variable Name `selected_time`
  - `DLV - timestamp` with Data Layer Variable Name `timestamp`
  - `DLV - selected_datetime` with Data Layer Variable Name `selected_datetime`
  - `DLV - selected_location` with Data Layer Variable Name `selected_location`
  - `DLV - booked_datetime` with Data Layer Variable Name `booked_datetime`
  - `DLV - booked_location` with Data Layer Variable Name `booked_location`
  - `DLV - form_error` with Data Layer Variable Name `form_error`

2. Create a single Custom Event Trigger

- Triggers → New → Trigger Type: Custom Event
- Event name: `rg_os_.*`
- Check "Use regex matching"
- Name it `OpenChair Events`

3. Create a GA4 Event tag (catch-all)

- Tags → New → Tag Type: Google Analytics: GA4 Event
- Configuration Tag: select your GA4 Configuration tag
- Event Name: `{{Event}}` (built-in variable) to pass through the data layer event name
- Event Parameters: add the variables you created; they will populate when present
  - `selected_date` → `{{DLV - selected_date}}`
  - `selected_time` → `{{DLV - selected_time}}`
  - `timestamp` → `{{DLV - timestamp}}`
  - `selected_datetime` → `{{DLV - selected_datetime}}`
  - `selected_location` → `{{DLV - selected_location}}`
  - `booked_datetime` → `{{DLV - booked_datetime}}`
  - `booked_location` → `{{DLV - booked_location}}`
  - `form_error` → `{{DLV - form_error}}`
- Triggering: `OpenChair Events`

Notes

- You can also create separate tags per event if you prefer specific mappings. The event names are: `rg_os_opened`, `rg_os_find_appointments_click`, `rg_os_appt_selection`, `rg_os_form_successful`, plus `rg_os_form_error` for failures.
- The widget pushes objects like:

```js
{ event: 'rg_os_find_appointments_click', selected_date: '2025-08-20', selected_time: '10:00', timestamp: '2025-08-20T10:00:00Z' }
{ event: 'rg_os_form_successful', booked_datetime: '2025-08-20T10:00:00Z', booked_location: 'Downtown' }
```

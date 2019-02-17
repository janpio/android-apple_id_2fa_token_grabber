# android-sms_forwarder-app-template

This is an Android app template that can read received SMS to extract and forward an Apple ID 2FA token to a specified API endpoint.

## ⚠️ Caution

This app template is not meant to be published to Google Play Store. It is to be used as a base to develop a single use, personal app to solve a specific problem only.

## Implementation Notes

### Receive SMS

#### Variant a

- https://developer.android.com/reference/android/Manifest.permission_group#SMS
- https://developer.android.com/reference/android/Manifest.permission#READ_SMS
- https://developer.android.com/reference/android/provider/Telephony.Sms
- https://developer.android.com/reference/android/telephony/SmsManager

Might be difficult because:
- https://support.google.com/googleplay/android-developer/answer/9047303
Shouldn't affect us because goal is not to put app into Play Store.

- https://android.jlelse.eu/detecting-sending-sms-on-android-8a154562597f
- Workaround for possible limitation: https://medium.com/@giuseppe.modugno/this-method-registering-a-broadcastreceiver-in-the-manifest-doesnt-work-on-certain-phones-535585ca3982
- https://github.com/JoaquimLey/sms-parsing

#### Variant b

- https://developers.google.com/identity/sms-retriever/overview
- https://developers.google.com/identity/sms-retriever/request
- https://developers.google.com/identity/sms-retriever/verify
- https://www.twilio.com/docs/sms/app-verification

Probably not usable because:
> The SMS retrieval task will listen for **up to five minutes** for an SMS message that contains a **unique string that identifies your app**.

Yep, as we don't control the SMS we can fulfill this requirement: https://developers.google.com/identity/sms-retriever/verify#1_construct_a_verification_message

### Send to API

- Background service?
- Can we _always_ react to SMS and reliably send them to an API?

## Usage

1. Adapt `configuration.java` to contain your API endpoint where to send a received Apple ID 2FA token
1. Build the app and run it on your local device by running: `fastlane build`
1. Keep your device plugged in and logged in with the SIM card of your Apple ID


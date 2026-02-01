# Strong and Savage Nutrition - SMS Program Documentation

**[Privacy Policy](privacy-policy.md)** | **[Terms of Service](terms-of-service.md)**

---

## Program Overview

**Business Name:** Strong and Savage Nutrition
**Program Type:** Transactional/Informational SMS Notifications
**Use Case:** Meal ordering platform for weekly meal prep service

Strong and Savage Nutrition is a web-based meal ordering platform that connects a meal preparation business with its clients. The SMS program sends notifications about new weekly menus and order updates to clients who have explicitly opted in to receive text messages.

---

## Message Types

The SMS program sends the following types of messages:

| Message Type | Purpose | Frequency |
|-------------|---------|-----------|
| Opt-In Request | Request client consent for SMS notifications | Once per client (or upon admin re-request) |
| Menu Notification | Alert clients when a new weekly menu is available | Weekly (typically 1x per week) |
| Order Confirmation | Confirm order placement or updates | As needed when orders are placed |

**Estimated Message Volume:** Low volume, typically 1-3 messages per client per week during active menu periods.

---

## Opt-In Flow

### How Clients Opt In

Clients must provide explicit consent before receiving any SMS notifications. The opt-in process follows these steps:

1. **Admin Initiates Request**
   The business administrator sends an opt-in request to clients via the admin dashboard.

2. **Client Receives Opt-In Request**
   The client receives an SMS with the following message:

   > Strong and Savage Nutrition: Hi [Client Name]! We'd like to send you text notifications about new menus and orders.
   >
   > Reply YES to subscribe or STOP to opt out. Reply HELP for help. Msg freq varies. Msg & data rates may apply.

3. **Client Provides Consent**
   The client must reply with an affirmative keyword to opt in:
   - `YES`
   - `START`
   - `SUBSCRIBE`
   - `OPTIN`
   - `OPT-IN`
   - `UNSTOP`

4. **Confirmation Sent**
   Upon opting in, the client receives a confirmation message:

   > Strong and Savage Nutrition: You're now subscribed! You'll receive menu and order updates. Reply HELP for help, STOP to cancel. Msg freq varies. Msg & data rates may apply.

5. **Consent Recorded**
   The system records:
   - Opt-in status (`smsOptedIn = true`)
   - Timestamp of consent (`smsOptedInAt`)
   - Client phone number (E.164 format)

### Consent Requirements

- **No pre-checked boxes:** Clients must actively reply to opt in
- **Clear disclosure:** Message rates disclaimer included in opt-in request
- **Single opt-in:** One affirmative response required
- **No shared consent:** SMS consent is separate from email notifications

---

## Opt-Out Flow

### How Clients Opt Out

Clients can opt out at any time by replying with any of the following standard keywords:

- `STOP`
- `STOPALL`
- `UNSUBSCRIBE`
- `CANCEL`
- `END`
- `QUIT`

### HELP Keyword Support

Clients can reply `HELP` or `INFO` at any time to receive program information:

> Strong and Savage Nutrition: Weekly meal prep ordering. Reply YES to subscribe, STOP to cancel. Msg freq varies. Msg & data rates may apply. Contact: strongandsavagenutrition.com

### Opt-Out Confirmation

When a client opts out, they receive an immediate confirmation:

> Strong and Savage Nutrition: You've been unsubscribed and will no longer receive messages. Reply START to re-subscribe.

### Opt-Out Processing

- Opt-out requests are processed automatically via webhook
- Client record is updated immediately (`smsOptedIn = false`)
- Timestamp is recorded (`smsOptedOutAt`)
- No further messages are sent until client re-opts in
- Clients can re-subscribe at any time by replying `START` or `YES`

---

## Sample Messages

### Opt-In Request
```
Strong and Savage Nutrition: Hi Sarah! We'd like to send you text
notifications about new menus and orders.

Reply YES to subscribe or STOP to opt out. Reply HELP for help.
Msg freq varies. Msg & data rates may apply.
```

### Menu Notification
```
Strong and Savage Nutrition: Hi Sarah! Weekly Menu is now available.
Order by Sun, Feb 2, 6:00 PM: https://example.com/order/abc123?token=xyz

Reply HELP for help, STOP to cancel. Msg freq varies.
Msg & data rates may apply.
```

### Opt-In Confirmation
```
Strong and Savage Nutrition: You're now subscribed! You'll receive
menu and order updates. Reply HELP for help, STOP to cancel.
Msg freq varies. Msg & data rates may apply.
```

### Opt-Out Confirmation
```
Strong and Savage Nutrition: You've been unsubscribed and will no
longer receive messages. Reply START to re-subscribe.
```

### HELP Response
```
Strong and Savage Nutrition: Weekly meal prep ordering. Reply YES to
subscribe, STOP to cancel. Msg freq varies. Msg & data rates may apply.
Contact: strongandsavagenutrition.com
```

---

## Technical Implementation

### Consent Storage

Client consent is stored in a database with the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `smsOptedIn` | Boolean | Current opt-in status |
| `smsOptedInAt` | DateTime | Timestamp when client opted in |
| `smsOptedOutAt` | DateTime | Timestamp when client opted out |
| `smsOptInSentAt` | DateTime | Timestamp when opt-in request was sent |
| `phoneNumber` | String | Phone number in E.164 format |

### Webhook Processing

Inbound SMS messages are processed via Twilio webhook:

1. Message received at `/api/webhooks/twilio/sms`
2. Phone number normalized to E.164 format
3. Client lookup by phone number
4. Keyword detection (opt-in/opt-out)
5. Database update with timestamp
6. TwiML response sent to client

### Consent Enforcement

Before sending any SMS notification:

1. System checks `smsOptedIn` status
2. Messages only sent if `smsOptedIn = true`
3. Clients without consent receive email only (if available)
4. Skipped SMS are logged with reason

---

## Compliance Features

### TCPA Compliance
- Express written consent obtained before sending messages
- Clear opt-out instructions in opt-in request
- Immediate opt-out processing
- Consent records maintained with timestamps

### CTIA Guidelines
- Standard STOP keyword support (STOP, STOPALL, UNSUBSCRIBE, CANCEL, END, QUIT)
- Standard HELP keyword support (HELP, INFO) - returns program info and support contact
- Standard START keyword support for re-subscription
- Message frequency disclosure (weekly menu notifications)
- Message and data rates disclaimer
- Clear program identification in all messages

### CAN-SPAM (for MMS)
- Business identification in messages
- Physical address available on website
- Opt-out mechanism in every message

---

## Contact Information

**Business:** Strong and Savage Nutrition
**Website:** strongandsavagenutrition.com
**Support:** Available via the meal ordering platform
**Opt-Out:** Reply STOP to any message

**Legal Documents:**
- [Privacy Policy](privacy-policy.md)
- [Terms of Service](terms-of-service.md)

---

## Program Terms

By opting in to SMS notifications from Strong and Savage Nutrition, you agree to receive text messages about:
- New weekly menu availability
- Order confirmations and updates
- Important service announcements

**Message Frequency:** Varies; typically 1-3 messages per week during active menu periods.

**Message & Data Rates:** Standard message and data rates may apply based on your mobile carrier plan.

**Opt-Out:** Reply STOP at any time to unsubscribe from SMS notifications. You will receive a confirmation message and no further texts will be sent.

**Help:** Reply HELP for assistance or contact us through the ordering platform.

**Privacy:** Your phone number is used solely for order-related notifications and is not shared with third parties.

---

*Last Updated: January 2026*

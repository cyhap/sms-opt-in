# Strong and Savage Nutrition - SMS Program

**[Privacy Policy](privacy-policy.md)** | **[Terms of Service](terms-of-service.md)**

---

## Join Strong and Savage Nutrition Text Updates

Text **MENU** to **[YOUR TOLL-FREE NUMBER]** to receive text notifications about weekly menus, ordering links, and order updates.

After you text MENU, we will send a confirmation message. Reply **YES** to confirm your subscription.

---

### Program Details

- **Message frequency:** Up to 4 msgs/wk
- **Costs:** Msg & data rates may apply
- **Opt out:** Reply STOP to cancel at any time
- **Help:** Reply HELP for help

By subscribing, you agree to our [Terms of Service](terms-of-service.md) and [Privacy Policy](privacy-policy.md).

---

## Program Overview

**Business Name:** Strong and Savage Nutrition
**Program Type:** Transactional/Informational SMS Notifications
**Use Case:** Meal ordering platform for weekly meal prep service

Strong and Savage Nutrition is a web-based meal ordering platform that connects our meal preparation business with clients. The SMS program sends notifications about weekly menus, ordering links, and order updates to clients who have explicitly opted in via double opt-in.

---

## Message Types

| Message Type | Purpose | Frequency |
|-------------|---------|-----------|
| Opt-In Confirmation | Confirm subscription request (double opt-in) | Once per subscription |
| Menu Notification | Alert clients when a new weekly menu is available | Weekly |
| Order Updates | Confirm order placement or updates | As needed |

**Estimated Message Volume:** Up to 4 messages per week during active menu periods.

---

## Opt-In Flow (Double Opt-In via Text)

### How Clients Opt In

Clients must provide explicit consent through a two-step double opt-in process:

1. **Client Initiates**
   Client texts **MENU** to our toll-free number.

2. **Confirmation Request Sent**
   Client receives:

   > Strong and Savage Nutrition: Reply YES to confirm subscription for weekly menus, ordering links, and order updates. Msg freq: up to 4 msgs/wk. Msg & data rates may apply. Reply STOP to cancel, HELP for help.

3. **Client Confirms**
   Client replies **YES** to confirm subscription.

4. **Subscription Confirmed**
   Client receives:

   > Strong and Savage Nutrition: You're subscribed for weekly menus, ordering links, and order updates. Msg freq: up to 4 msgs/wk. Reply STOP to cancel, HELP for help. Msg & data rates may apply.

5. **Consent Recorded**
   The system records:
   - Opt-in status
   - Timestamp of consent
   - Client phone number (E.164 format)

### Opt-In Keywords

| Keyword | Action |
|---------|--------|
| **MENU** | Initiate subscription (sends confirmation request) |
| **YES** | Confirm subscription (completes double opt-in) |

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

### Opt-Out Confirmation

When a client opts out, they receive an immediate confirmation:

> Strong and Savage Nutrition: You've been unsubscribed and will no longer receive messages. Reply START to re-subscribe.

### Opt-Out Processing

- Opt-out requests are processed automatically via webhook
- Client record is updated immediately
- Timestamp is recorded
- No further messages are sent until client re-opts in

---

## HELP Keyword Support

Clients can reply `HELP` or `INFO` at any time to receive program information:

> Strong and Savage Nutrition: Text MENU to subscribe for weekly menus, ordering links, and order updates. Msg freq: up to 4 msgs/wk. Msg & data rates may apply. Reply STOP to cancel. Contact: strongandsavagenutrition.com

---

## Sample Messages

### Opt-In Confirmation Request (after texting MENU)
```
Strong and Savage Nutrition: Reply YES to confirm subscription for
weekly menus, ordering links, and order updates. Msg freq: up to 4
msgs/wk. Msg & data rates may apply. Reply STOP to cancel, HELP for help.
```

### Subscription Confirmed (after replying YES)
```
Strong and Savage Nutrition: You're subscribed for weekly menus,
ordering links, and order updates. Msg freq: up to 4 msgs/wk.
Reply STOP to cancel, HELP for help. Msg & data rates may apply.
```

### Menu Notification
```
Strong and Savage Nutrition: Hi Sarah! Weekly Menu is now available.
Order by Sun, Feb 02, 18:00: https://example.com/order/abc123

Reply STOP to cancel, HELP for help. Msg & data rates may apply.
```

### Opt-Out Confirmation
```
Strong and Savage Nutrition: You've been unsubscribed and will no
longer receive messages. Reply START to re-subscribe.
```

### HELP Response
```
Strong and Savage Nutrition: Text MENU to subscribe for weekly menus,
ordering links, and order updates. Msg freq: up to 4 msgs/wk.
Msg & data rates may apply. Reply STOP to cancel.
Contact: strongandsavagenutrition.com
```

---

## Technical Implementation

### Consent Storage

Client consent is stored in a database with the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `smsOptedIn` | Boolean | Current opt-in status |
| `smsOptedInAt` | DateTime | Timestamp when client confirmed opt-in |
| `smsOptedOutAt` | DateTime | Timestamp when client opted out |
| `smsOptInSentAt` | DateTime | Timestamp when confirmation request was sent |
| `phoneNumber` | String | Phone number in E.164 format |

### Double Opt-In Flow

1. Client texts MENU to toll-free number
2. Webhook receives message at `/api/webhooks/twilio/sms`
3. System sends confirmation request, updates `smsOptInSentAt`
4. Client replies YES
5. System confirms `smsOptInSentAt` exists, updates `smsOptedIn = true` and `smsOptedInAt`
6. Confirmation message sent to client

### Consent Enforcement

Before sending any SMS notification:

1. System checks `smsOptedIn` status
2. Messages only sent if `smsOptedIn = true`
3. Clients without consent receive email only (if available)

---

## Compliance Features

### TCPA Compliance
- Express written consent via double opt-in (text MENU, reply YES)
- Clear opt-out instructions in all messages
- Immediate opt-out processing
- Consent records maintained with timestamps

### CTIA Guidelines
- Single advertised opt-in keyword (MENU)
- Standard STOP keyword support (STOP, STOPALL, UNSUBSCRIBE, CANCEL, END, QUIT)
- Standard HELP keyword support (HELP, INFO)
- Message frequency disclosure (up to 4 msgs/wk)
- Message and data rates disclaimer
- Clear program identification in all messages

---

## Contact Information

**Business:** Strong and Savage Nutrition
**Website:** strongandsavagenutrition.com
**Support:** Available via the meal ordering platform
**Opt-Out:** Reply STOP to any message
**Help:** Reply HELP to any message

**Legal Documents:**
- [Privacy Policy](privacy-policy.md)
- [Terms of Service](terms-of-service.md)

---

## Program Terms

By opting in to SMS notifications from Strong and Savage Nutrition, you agree to receive text messages about:
- Weekly menu availability
- Ordering links
- Order updates

**Message Frequency:** Up to 4 messages per week during active menu periods.

**Message & Data Rates:** Standard message and data rates may apply based on your mobile carrier plan.

**Opt-Out:** Reply STOP at any time to unsubscribe from SMS notifications. You will receive a confirmation message and no further texts will be sent.

**Help:** Reply HELP for assistance or contact us through the ordering platform.

**Privacy:** Your phone number is used solely for order-related notifications and is not shared with third parties.

---

*Last Updated: January 2026*

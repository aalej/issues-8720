# Repro for iss 8720

## Versions

firebase-tools: v14.6.0<br>
node: v20.19.1<br>
platform: macOS 15.5

## Steps to reproduce

1. Run `firebase logout`
   - Run `gcloud auth revoke` and `gcloud auth application-default revoke` if you have `gcloud`
1. Create and populate `./service-account.json` with service account key values
1. Run `export GOOGLE_APPLICATION_CREDENTIALS=./service-account.json`
   - Feel free to change the contents of `service-account.json`
1. Run `firebase emulators:start --only=auth,firestore,functions,extensions --project=demo-project`

## Notes

If you have `gcloud` CLI installed you might want to run the ff commands since the emulators picks up the ADC from `gcloud`

- `gcloud auth revoke`
- `gcloud auth application-default revoke`

### Running different versions

#### 14.2.0 - ok

```
$ firebase --version
14.2.0
$ export GOOGLE_APPLICATION_CREDENTIALS=./service-account.json
$ firebase emulators:start --only=auth,firestore,functions,extensions --project=demo-project
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
i  emulators: Starting emulators: auth, functions, firestore, extensions
i  emulators: Detected demo project ID "demo-project", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail.
⚠  Function 'createPortalLink' is missing a trigger in extension.yaml. Please add one, as triggers defined in code are ignored.
⚠  Function 'handleWebhookEvents' is missing a trigger in extension.yaml. Please add one, as triggers defined in code are ignored.
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
⚠  functions: Application Default Credentials detected. Non-emulated services will access production using these credentials. Be careful!
⚠  firestore: Cloud Firestore Emulator does not support multiple databases yet.
⚠  firestore: Did not find a Cloud Firestore rules file specified in a firebase.json config file.
⚠  firestore: The emulator will default to allowing all reads and writes. Learn more about this option: https://firebase.google.com/docs/emulator-suite/install_and_configure#security_rules_configuration.
i  firestore: Firestore Emulator logging to firestore-debug.log
✔  firestore: Firestore Emulator UI websocket is running on 9150.
i  functions: Watching "/Users/PATH/.cache/firebase/extensions/invertase/firestore-stripe-payments@0.3.11/functions" for Cloud Functions...
✔  functions: Loaded functions definitions from source: createCustomer, createCheckoutSession, createPortalLink, handleWebhookEvents, onUserDeleted, onCustomerDataDeleted.
✔  functions[us-central1-ext-stripe-createCustomer]: auth function initialized.
✔  functions[us-central1-ext-stripe-createCheckoutSession]: firestore function initialized.
✔  functions[us-central1-ext-stripe-createPortalLink]: http function initialized (http://127.0.0.1:5001/demo-project/us-central1/ext-stripe-createPortalLink).
✔  functions[us-central1-ext-stripe-handleWebhookEvents]: http function initialized (http://127.0.0.1:5001/demo-project/us-central1/ext-stripe-handleWebhookEvents).
✔  functions[us-central1-ext-stripe-onUserDeleted]: auth function initialized.
✔  functions[us-central1-ext-stripe-onCustomerDataDeleted]: firestore function initialized.

┌─────────────────────────────────────────────────────────────┐
│ ✔  All emulators ready! It is now safe to connect your app. │
│ i  View Emulator UI at http://127.0.0.1:4000/               │
└─────────────────────────────────────────────────────────────┘

┌────────────────┬────────────────┬──────────────────────────────────┐
│ Emulator       │ Host:Port      │ View in Emulator UI              │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Authentication │ 127.0.0.1:9099 │ http://127.0.0.1:4000/auth       │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Functions      │ 127.0.0.1:5001 │ http://127.0.0.1:4000/functions  │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Firestore      │ 127.0.0.1:8080 │ http://127.0.0.1:4000/firestore  │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Extensions     │ 127.0.0.1:5001 │ http://127.0.0.1:4000/extensions │
└────────────────┴────────────────┴──────────────────────────────────┘
  Emulator Hub host: 127.0.0.1 port: 4400
  Other reserved ports: 4500, 9150
┌─────────────────────────┬────────────────────────────────────────────┬─────────────────────────────────────────┐
│ Extension Instance Name │ Extension Ref                              │ View in Emulator UI                     │
├─────────────────────────┼────────────────────────────────────────────┼─────────────────────────────────────────┤
│ stripe                  │ invertase/firestore-stripe-payments@0.3.11 │ http://127.0.0.1:4000/extensions/stripe │
└─────────────────────────┴────────────────────────────────────────────┴─────────────────────────────────────────┘
Issues? Report them at https://github.com/firebase/firebase-tools/issues and attach the *-debug.log files.

^C
i  emulators: Received SIGINT (Ctrl-C) for the first time. Starting a clean shutdown.
i  emulators: Please wait for a clean shutdown or send the SIGINT (Ctrl-C) signal again to stop right now.
i  emulators: Shutting down emulators.
i  ui: Stopping Emulator UI
i  extensions: Stopping Extensions Emulator
i  functions: Stopping Functions Emulator
i  firestore: Stopping Firestore Emulator
i  auth: Stopping Authentication Emulator
i  eventarc: Stopping Eventarc Emulator
i  tasks: Stopping Cloud Tasks Emulator
i  hub: Stopping emulator hub
i  logging: Stopping Logging Emulator
```

#### 14.2.1 - ok

```
$ firebase --version
14.2.1
$ export GOOGLE_APPLICATION_CREDENTIALS=./service-account.json
$ firebase emulators:start --only=auth,firestore,functions,extensions --project=demo-project
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
i  emulators: Starting emulators: auth, functions, firestore, extensions
i  emulators: Detected demo project ID "demo-project", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail.
⚠  Function 'createPortalLink' is missing a trigger in extension.yaml. Please add one, as triggers defined in code are ignored.
⚠  Function 'handleWebhookEvents' is missing a trigger in extension.yaml. Please add one, as triggers defined in code are ignored.
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
⚠  functions: Application Default Credentials detected. Non-emulated services will access production using these credentials. Be careful!
⚠  firestore: Cloud Firestore Emulator does not support multiple databases yet.
⚠  firestore: Did not find a Cloud Firestore rules file specified in a firebase.json config file.
⚠  firestore: The emulator will default to allowing all reads and writes. Learn more about this option: https://firebase.google.com/docs/emulator-suite/install_and_configure#security_rules_configuration.
i  firestore: Firestore Emulator logging to firestore-debug.log
✔  firestore: Firestore Emulator UI websocket is running on 9150.
i  functions: Watching "/Users/PATH/.cache/firebase/extensions/invertase/firestore-stripe-payments@0.3.11/functions" for Cloud Functions...
✔  functions: Loaded functions definitions from source: createCustomer, createCheckoutSession, createPortalLink, handleWebhookEvents, onUserDeleted, onCustomerDataDeleted.
✔  functions[us-central1-ext-stripe-createCustomer]: auth function initialized.
✔  functions[us-central1-ext-stripe-createCheckoutSession]: firestore function initialized.
✔  functions[us-central1-ext-stripe-createPortalLink]: http function initialized (http://127.0.0.1:5001/demo-project/us-central1/ext-stripe-createPortalLink).
✔  functions[us-central1-ext-stripe-handleWebhookEvents]: http function initialized (http://127.0.0.1:5001/demo-project/us-central1/ext-stripe-handleWebhookEvents).
✔  functions[us-central1-ext-stripe-onUserDeleted]: auth function initialized.
✔  functions[us-central1-ext-stripe-onCustomerDataDeleted]: firestore function initialized.

┌─────────────────────────────────────────────────────────────┐
│ ✔  All emulators ready! It is now safe to connect your app. │
│ i  View Emulator UI at http://127.0.0.1:4000/               │
└─────────────────────────────────────────────────────────────┘

┌────────────────┬────────────────┬──────────────────────────────────┐
│ Emulator       │ Host:Port      │ View in Emulator UI              │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Authentication │ 127.0.0.1:9099 │ http://127.0.0.1:4000/auth       │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Functions      │ 127.0.0.1:5001 │ http://127.0.0.1:4000/functions  │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Firestore      │ 127.0.0.1:8080 │ http://127.0.0.1:4000/firestore  │
├────────────────┼────────────────┼──────────────────────────────────┤
│ Extensions     │ 127.0.0.1:5001 │ http://127.0.0.1:4000/extensions │
└────────────────┴────────────────┴──────────────────────────────────┘
  Emulator Hub host: 127.0.0.1 port: 4400
  Other reserved ports: 4500, 9150
┌─────────────────────────┬────────────────────────────────────────────┬─────────────────────────────────────────┐
│ Extension Instance Name │ Extension Ref                              │ View in Emulator UI                     │
├─────────────────────────┼────────────────────────────────────────────┼─────────────────────────────────────────┤
│ stripe                  │ invertase/firestore-stripe-payments@0.3.11 │ http://127.0.0.1:4000/extensions/stripe │
└─────────────────────────┴────────────────────────────────────────────┴─────────────────────────────────────────┘
Issues? Report them at https://github.com/firebase/firebase-tools/issues and attach the *-debug.log files.

^C
i  emulators: Received SIGINT (Ctrl-C) for the first time. Starting a clean shutdown.
i  emulators: Please wait for a clean shutdown or send the SIGINT (Ctrl-C) signal again to stop right now.
i  emulators: Shutting down emulators.
i  ui: Stopping Emulator UI
i  extensions: Stopping Extensions Emulator
i  functions: Stopping Functions Emulator
i  firestore: Stopping Firestore Emulator
i  auth: Stopping Authentication Emulator
i  eventarc: Stopping Eventarc Emulator
i  tasks: Stopping Cloud Tasks Emulator
i  hub: Stopping emulator hub
i  logging: Stopping Logging Emulator
```

#### 14.2.2 - error

```
$ firebase --version
14.2.2
$ export GOOGLE_APPLICATION_CREDENTIALS=./service-account.json
$ firebase emulators:start --only=auth,firestore,functions,extensions --project=demo-project
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
i  emulators: Starting emulators: auth, functions, firestore, extensions
i  emulators: Detected demo project ID "demo-project", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail.
i  emulators: Shutting down emulators.

Error: Errors while reading 'extensions' in 'firebase.json'
- Unable to refresh auth: not yet authenticated.
```

#### 14.3.0 - error

```
$ firebase --version
14.3.0
$ export GOOGLE_APPLICATION_CREDENTIALS=./service-account.json
$ firebase emulators:start --only=auth,firestore,functions,extensions --project=demo-project
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
i  emulators: Starting emulators: auth, functions, firestore, extensions
i  emulators: Detected demo project ID "demo-project", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail.
i  emulators: Shutting down emulators.

Error: Errors while reading 'extensions' in 'firebase.json'
- Unable to refresh auth: not yet authenticated.
```

#### 14.6.0 - error

```
$ firebase --version
14.6.0
$ export GOOGLE_APPLICATION_CREDENTIALS=./service-account.json
$ firebase emulators:start --only=auth,firestore,functions,extensions --project=demo-project
⚠  functions: The functions emulator is configured but there is no functions source directory. Have you run firebase init functions?
i  emulators: Starting emulators: auth, functions, firestore, extensions
i  emulators: Detected demo project ID "demo-project", emulated services will use a demo configuration and attempts to access non-emulated services for this project will fail.
i  emulators: Shutting down emulators.

Error: Errors while reading 'extensions' in 'firebase.json'
- Unable to refresh auth: not yet authenticated.
```

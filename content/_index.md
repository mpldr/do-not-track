# `DO_NOT_TRACK`

In this day and age, more and more tools have some kind of telemetry or
another. This usually comes with quite a bit of
[community](https://github.com/golang/go/discussions/58409)
[backlash](https://github.com/audacity/audacity/pull/835). This page does not
exist to be a place for debate about the ups and downs, or the legality of
various models of implementing telemetry, but rather to help developers make
opting out easy with a simple, universally available setting.

## How it works

The `DO_NOT_TRACK` environment variable acts in a very similar fashion to
browser's `DNT` header, in that it's presence signals a desire not to be
tracked. Explicit consent can however, override this.

To put it into code:

```go
if value, present os.LookupEnv("DO_NOT_TRACK"); present {
	if !settings.ExplicitlyAllowedTracking() {
		// do _not_ track the user, environment variable is present
		return
	}
	// user has allowed this application to collect telemetry data
}
```

By doing this, you allow your user to set their own default

## What is telemetry?

Telemetry is the automated collection of data and it's transmission to
a central receiver (usually, the developers). This includes, but is in no way
limited to:
- Usage patterns
- Error/Crash logs
- Performance metrics
- System information

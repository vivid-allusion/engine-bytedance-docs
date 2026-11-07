---
title: "The lifecycle"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/The_lifecycle"
---

Mount the listener via `on`, and unmount the listener via `off`.

<span id="init"></span>
## init

Listener instance has been initialized.

```typescript
 client('on', 'init', () => {
    ...
 })
```


<span id="start"></span>
## start

Turn on reporting for listener instances.

```typescript
 client('on', 'start', () => {
    ...
 })
```


<span id="beforeConfig"></span>
## beforeConfig

The new configuration can be obtained before listening for instance configuration changes.

```typescript
client('on', 'beforeConfig', (config: Partial<Config>) => {
    ...
})

```


<span id="config"></span>
## config

Listen for the instant after an instance configuration change.

```typescript
 client('on', 'config', () => {
    ...
 })
```


<span id="provide"></span>
## provide

Listen for the moment when a property is mounted to the instance; at that moment, the property name can be obtained.

```typescript
 client('on', 'provide', (name: string) => {
    ...
 })
```


<span id="report"></span>
## report

When the monitored event is sent by the Monitoring plugin, this can be used to provide additional context for the event. If a Falsy type is returned, the event will not be reported.

```typescript
 client('on', 'report', (ev: ReportEvent): ReportEvent | Falsy => {
    ...
 })

export type Falsy = false | null | undefined
```


<span id="beforeBuild"></span>
## beforeBuild

At the moment just before the event is wrapped with context, you can access the data that is about to be wrapped. If the function returns a Falsy type, the event will not be reported.

```typescript
 client('on', 'beforeBuild', (ev: ReportEvent): ReportEvent | Falsy => {
    ...
 })

export type Falsy = false | null | undefined
```


<span id="build"></span>
## build

Immediately after the event is wrapped with context, you can access the data that is about to be reported. If a Falsy type is returned, the data will not be reported.

```typescript
 client('on', 'build', (ev: SendEvent): SendEvent | Falsy => {
    ...
 })

export type Falsy = false | null | undefined
```


<span id="beforeSend"></span>
## beforeSend

At the moment before the event is sent, if the listener returns a Falsy type, the event will not be reported.

```typescript
 client('on', 'beforeSend', (ev: SendEvent): SendEvent | Falsy => {
    ...
 })

export type Falsy = false | null | undefined
```


<span id="send"></span>
## send

Callback after the register event is sent.

```typescript
 client('on', 'send', (e: Callback<SendEvent>) => {
    ...
 })
  
interface Callback<T> {
  (arg: T): void
}
```


<span id="beforeDestroy"></span>
## beforeDestroy

Callback before the destruction of a registered instance.

```typescript
 client('on', 'beforeDestroy', () => {
    ...
 })
```


<span id=".U2VuZEV2ZW50ICYmIFJlcG9ydEV2ZW50IOexu-Wei-WjsOaYjg=="></span>
## SendEvent and ReportEvent type declarations

```typescript
// See reporting format for details on each type.
export type SendEvent =
  | CustomReport
  | HttpReport
  | JsErrorReport
  | PageviewReport
  | PerformanceReport
  | PerformanceLongTaskReport
  | PerformanceTimingReport
  | ResourceErrorReport
  | ResourceReport
  | SriReport
  | BlankReport

export type WebReport = Omit<SendEvent,'common'> 

export type ReportEvent<T extends WebReport> = T & {
  // For the specific common format, refer to the reporting format
  extra?: Partial<Common>
  // Allows reporting additional context to override the assembled context, mainly in pre-collection and preloading scenarios
  overrides?: Partial<Common>
}
```

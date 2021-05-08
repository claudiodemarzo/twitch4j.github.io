---
title: Subscriptions - Get all subscribers of a channel
layout: docs
weight : 55
menu: 
  docs:
    parent: API - Helix
---

# Get all subscribers of a channel

## Description

Get all of a broadcaster’s subscriptions.

Required OAuth Scope: `channel:read:subscriptions`

## Method Definition

```java
@RequestLine("GET /subscriptions?broadcaster_id={broadcaster_id}&after={after}&before={before}&first={first}")
@Headers("Authorization: Bearer {token}")
HystrixCommand<SubscriptionList> getSubscriptions(
	@Param("token") String authToken,
	@Param("broadcaster_id") Long broadcasterId,
	@Param("after") String after,
	@Param("before") String before,
	@Param("first") Integer limit
);
```

*Required Parameters*

| Name          | Type      | Description  |
| ------------- |:---------:| -----------------:|
| token | string | bearer token |
| broadcaster_id | number | ID of the broadcaster. Must match the User ID in the Bearer token |

*Optional Parameters*

| Name          | Type      | Description  |
| ------------- |:---------:| -----------------:|
| after | string | Cursor for forward pagination: tells the server where to start fetching the next set of results, in a multi-page response. The cursor value specified here is from the pagination response field of a prior query. |
| before | string | Cursor for backward pagination: tells the server where to start fetching the next set of results, in a multi-page response. The cursor value specified here is from the pagination response field of a prior query. |
| limit | string | Maximum number of objects to return. Maximum: 100. Default: 20. |

## Code-Snippets

{{<codeblocks>}}
{{<code Java>}}
```java
SubscriptionList resultList = client.getHelix().getSubscriptions(ACCESS_TOKEN, CHANNEL_ID, null, null,null).execute();
resultList.getSubscriptions().forEach(subscription -> {
	System.out.println("Subscriber: "+subscription.getUserName());
});
```
{{</code>}}
{{<code Groovy>}}
```groovy
def resultList = client.helix.getSubscriptions(ACCESS_TOKEN, CHANNEL_ID, null, null,null).execute()
resultList.subscriptions.forEach {
	System.out.println("Subscriber: ${it.userName}")
}
```
{{</code>}}
{{<code Kotlin>}}
```kotlin
val resultList = client.helix.getSubscriptions(ACCESS_TOKEN, CHANNEL_ID, null, null,null).execute()
resultList.subscriptions.forEach {
	println("Subscriber: ${it.userName}")
}
```
{{</code>}}
{{</codeblocks>}}


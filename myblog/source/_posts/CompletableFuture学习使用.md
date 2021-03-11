---
title: CompletableFuture学习使用
date: 2021-01-12 14:57:03
tags: java
---

# CompletableFuture
## 介绍
1.8以前是没有CompletableFuture的，之前是Future，我们是通过Future的get方法获取线程执行返回结果的，CompletableFuture拓展了Future。

使用场景：使用多线程执行结果之间有相互依赖关系，这时候就可以使用CompletableFuture了

CompletableFuture实现了两个接口，分别是Future和CompletionStage，下面主要是看下CompletionStage

<!--more-->

## 了解functions
首先了解下java.util.function里的几个接口

| 类名 | 方法 | 描述 |
| :--- | :--- | :--- |
| Function<T, R> | R apply(T t)、compose、andThen、identity() | 接受入参T，返回结果R|
| Consumer<T> | void accept(T t)、andThen | 接受入参T，无返回结果|
| Supplier<T> | T get() | 无入参，返回结果T|
| Predicate<T> | boolean test(T t)、and、negate、or、isEqual | 接受入参T，返回bool值|


## CompletionStage
| 方法 | 返回值 | 描述 |
| :--- | --- | --- |
| thenApply(Function<? super T,? extends U> fn) | CompletionStage<U> | |
| thenAccept(Consumer<? super T> action) | CompletionStage<Void> | |
| thenRun(Runnable action) | CompletionStage<Void> | |
| thenCombine(CompletionStage<? extends U> other, BiFunction<? super T,? super U,? extends V> fn) | CompletionStage<V> | |
| runAfterBoth(CompletionStage<?> other, Runnable action) | CompletionStage<Void> | |
| applyToEither(CompletionStage<? extends T> other, Function<? super T, U> fn) | CompletionStage<U> | |
| acceptEither(CompletionStage<? extends T> other, Consumer<? super T> action) | CompletionStage<Void> | |
| runAfterEither(CompletionStage<?> other, Runnable action) | CompletionStage<Void> | |
| thenCompose(Function<? super T, ? extends CompletionStage<U>> fn) | CompletionStage<U> | |
| whenComplete(BiConsumer<? super T, ? super Throwable> action) | CompletionStage<T> | |
| handle(BiFunction<? super T, Throwable, ? extends U> fn) | CompletionStage<U> | |

## 使用

```java

```
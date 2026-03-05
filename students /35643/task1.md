# Event-Driven Architecture Example: Food Delivery System

## Overview

This document describes a simple Event-Driven Architecture (EDA) for a
food delivery system. The system reacts to events such as order
creation, payment completion, and delivery updates.

Example platforms with similar architecture include Uber Eats and
DoorDash.

------------------------------------------------------------------------

# Architecture Components

## 1. Event

An **event** represents something that has already happened in the
system.

Examples: - OrderPlaced - PaymentCompleted - RestaurantAcceptedOrder -
DriverAssigned - OrderDelivered

Example event message:

``` json
{
  "event": "OrderPlaced",
  "order_id": 45821,
  "customer_id": 102,
  "restaurant_id": 56,
  "timestamp": "2026-03-05T14:00:00"
}
```

------------------------------------------------------------------------

## 2. Event Producer

An **event producer** generates events when actions occur.

Examples: - Order Service - Payment Service

Example: When a customer places an order, the **Order Service**
publishes the `OrderPlaced` event.

------------------------------------------------------------------------

## 3. Event Broker

The **event broker** receives events and distributes them to services
that are subscribed to them.

Common technologies: - Apache Kafka - RabbitMQ - Amazon EventBridge

Responsibilities: - Receive events - Store or queue events - Deliver
events to subscribers

------------------------------------------------------------------------

## 4. Event Consumers (Event Handlers)

Event consumers listen for events and perform actions.

Examples:

  Event                     Consumer               Action
  ------------------------- ---------------------- --------------------------
  OrderPlaced               Payment Service        Process payment
  PaymentCompleted          Restaurant Service     Send order to restaurant
  RestaurantAcceptedOrder   Delivery Service       Assign driver
  DriverAssigned            Notification Service   Notify customer
  OrderDelivered            Rating Service         Request feedback

------------------------------------------------------------------------

# Event Flow

## Step 1: Customer Places Order

Event generated:

    OrderPlaced

Consumers: - Payment Service - Notification Service

------------------------------------------------------------------------

## Step 2: Payment Completed

Event generated:

    PaymentCompleted

Consumers: - Restaurant Service - Analytics Service

------------------------------------------------------------------------

## Step 3: Restaurant Accepts Order

Event generated:

    RestaurantAcceptedOrder

Consumers: - Delivery Service - Notification Service

------------------------------------------------------------------------

## Step 4: Driver Assigned

Event generated:

    DriverAssigned

Consumers: - Tracking Service - Notification Service

------------------------------------------------------------------------

## Step 5: Order Delivered

Event generated:

    OrderDelivered

Consumers: - Rating Service - Analytics Service

------------------------------------------------------------------------

# Event Flow Diagram

    Customer
       |
       v
    Order Service
       |
       v
    Event Broker
       |
       +---- Payment Service
       |
       +---- Restaurant Service
       |
       +---- Delivery Service
       |
       +---- Notification Service

------------------------------------------------------------------------

# Advantages of Event-Driven Architecture

-   Loose coupling between services
-   Better scalability
-   Real-time processing
-   Easy integration of new services

Example: A **Fraud Detection Service** could later subscribe to
`PaymentCompleted` events without modifying existing services.

------------------------------------------------------------------------

# Summary

  Component   Role
  ----------- ------------------------------
  Event       Something that happened
  Producer    Creates and publishes events
  Broker      Routes events
  Consumer    Reacts to events

# quincadz

`quincadz` is the multi-tenant marketplace and merchant-operations skill. It is appropriate for systems where a customer shops across independent stores, merchants manage their own catalogues/orders, and platform staff govern the overall marketplace.

## Coverage

The guide defines tenant and role boundaries, Supabase/Postgres records and RLS, route groups, server actions/APIs, location and media handling, responsive customer/merchant/platform UX, analytics, operational controls and test cases.

## How to use it

Read `SKILL.md` with [`../STANDARDS.md`](../STANDARDS.md). Combine it with `make-ur-kdb` only if the system also needs its specific premium brand/storefront and private owner-control playbook.

## Core principle

Multi-tenancy is a database and authorization property, not a sidebar selection. Every record, query, upload and mutation must prove its store/role scope.

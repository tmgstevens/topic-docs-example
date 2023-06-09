# Owlshop-Orders

| Producing Team | Producing Service         | GDPR sensitive | Importance | Data type |
|----------------|---------------------------|----------------|------------|-----------|
| CloudHut       | quay.io/cloudhut/owl-shop | Yes            | Critical   | Protobuf  |

Protobuf representation of owlshop orders.

## Settings

| Setting    | Value   |
|------------|---------|
| Compaction | true    |
| Retention  | default |

## Key Schema

The key is the order UUID.

## Value Proto
```
syntax = "proto3";
package fake_models;

import "google/protobuf/timestamp.proto";
import "customer.proto";
import "address.proto";
option go_package = "pkg/protobuf";

message Order {
  int32 version = 1;
  string id = 2;
  google.protobuf.Timestamp created_at = 3;
  google.protobuf.Timestamp last_updated_at = 4;
  google.protobuf.Timestamp delivered_at = 5;
  google.protobuf.Timestamp completed_at = 6;

  Customer Customer = 7;
  int32 OrderValue = 8;

  message LineItem {
    string article_id = 1;
    string name = 2;
    int32 quantity = 3;
    string quantity_unit = 4;
    int32 unit_price = 5;
    int32 total_price = 6;
  }
  repeated LineItem line_items = 9;

  message Payment {
    string payment_id = 1;
    string method = 2;
  }
  Payment payment = 10;
  Address delivery_address = 11;
  int32 revision = 12;
}
```
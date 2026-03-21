# Dynamodb Table

Manage Dynamodb Table resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_dynamodb_table:
    basic-dynamodb-table:
      name: GameScores
      billing_mode: PROVISIONED
      read_capacity: 20
      write_capacity: 20
      hash_key: UserId
      range_key: GameTitle
      attribute:
        name: UserId
        type: S
      attribute:
        name: GameTitle
        type: S
      attribute:
        name: TopScore
        type: N
      ttl:
        attribute_name: TimeToExist
        enabled: true
      global_secondary_index:
        name: GameTitleIndex
        hash_key: GameTitle
        range_key: TopScore
        write_capacity: 10
        read_capacity: 10
        projection_type: INCLUDE
        non_key_attributes: 
          - UserId
      tags:
        Name: dynamodb-table-1
        Environment: production
```

## Basic Example containing Global Secondary Indexes using Multi-attribute keys pattern

```yaml
resource:
  aws_dynamodb_table:
    basic-dynamodb-table:
      name: TournamentMatches
      billing_mode: PROVISIONED
      read_capacity: 20
      write_capacity: 20
      hash_key: matchId
      attribute:
        name: matchId
        type: S
      attribute:
        name: tournamentId
        type: S
      attribute:
        name: region
        type: S
      attribute:
        name: round
        type: S
      attribute:
        name: bracket
        type: S
      attribute:
        name: playerId
        type: N
      attribute:
        name: matchDate
        type: S
      ttl:
        attribute_name: TimeToExist
        enabled: true
      global_secondary_index:
        name: TournamentRegionIndex
        key_schema:
          attribute_name: tournamentId
          key_type: HASH
        key_schema:
          attribute_name: region
          key_type: HASH
        key_schema:
          attribute_name: round
          key_type: RANGE
        key_schema:
          attribute_name: bracket
          key_type: RANGE
        key_schema:
          attribute_name: matchId
          key_type: RANGE
        write_capacity: 10
        read_capacity: 10
        projection_type: ALL
      global_secondary_index:
        name: PlayerMatchHistoryIndex
        key_schema:
          attribute_name: playerId
          key_type: HASH
        key_schema:
          attribute_name: matchDate
          key_type: RANGE
        key_schema:
          attribute_name: round
          key_type: RANGE
        write_capacity: 10
        read_capacity: 10
        projection_type: ALL
      tags:
        Name: dynamodb-table-1
        Environment: production
```

## Global Tables

```yaml
resource:
  aws_dynamodb_table:
    example:
      name: example
      hash_key: TestTableHashKey
      billing_mode: PAY_PER_REQUEST
      stream_enabled: true
      stream_view_type: NEW_AND_OLD_IMAGES
      attribute:
        name: TestTableHashKey
        type: S
      replica:
        region_name: us-east-2
      replica:
        region_name: us-west-2
```

## Replica Tagging

```yaml
data:
  aws_region:
    current:

data:
  aws_region:
    alternate:

data:
  aws_region:
    third:

resource:
  aws_dynamodb_table:
    example:
      billing_mode: PAY_PER_REQUEST
      hash_key: TestTableHashKey
      name: example-13281
      stream_enabled: true
      stream_view_type: NEW_AND_OLD_IMAGES
      attribute:
        name: TestTableHashKey
        type: S
      replica:
        region_name: ${data.aws_region.alternate.name}
      replica:
        region_name: ${data.aws_region.third.name}
        propagate_tags: true
      tags:
        Architect: Eleanor
        Zone: SW

resource:
  aws_dynamodb_tag:
    example:
      resource_arn: replaced-value
      key: Architect
      value: Gigi
```

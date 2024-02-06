validate a feature model with a CLI

# usage #

1. clone this repo
2. replace model.xml with your feature model
3. execute `./run.sh`
4. results file is created `results.json`

# dependencies #

1. java 17

# example #

## model.xml ##

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<featureModel>
  <struct>
    <and mandatory="true" name="Root">
      <graphics key="collapsed" value="false"/>
      <alt mandatory="true" name="FeatureA">
        <feature name="FeatureB"/>
        <feature name="FeatureC"/>
      </alt>
      <and mandatory="true" name="GoalA">
        <feature mandatory="true" name="GoalB"/>
        <feature mandatory="true" name="GoalC"/>
      </and>
    </and>
  </struct>
  <constraints>
    <rule>
      <imp>
        <var>GoalB</var>
        <var>FeatureB</var>
      </imp>
    </rule>
    <rule>
      <imp>
        <var>GoalC</var>
        <var>FeatureC</var>
      </imp>
    </rule>
  </constraints>
</featureModel>
```

## Result ##

```json
{
  "hasRedundantConstraints": false,
  "hasFalseOptionalConstraints": false,
  "hasDeadFeatures": true,
  "hasDeadConstraints": false,
  "hasUnsatisfiableConstraints": false,
  "hasDeadFeature": false,
  "featureModelElementsProperties": {
    "GoalA": [
      "DEAD",
      "MANDATORY"
    ],
    "GoalB": [
      "DEAD",
      "MANDATORY"
    ],
    "Root": [
      "DEAD",
      "MANDATORY"
    ],
    "FeatureC": [
      "DEAD"
    ],
    "FeatureB": [
      "DEAD"
    ],
    "FeatureA": [
      "DEAD",
      "GROUP"
    ],
    "GoalC": [
      "DEAD",
      "MANDATORY"
    ]
  },
  "hasFalseOptionalFeatures": false,
  "hasVoidModelConstraints": true,
  "hasIndeterminateHiddenFeatures": false
}
```

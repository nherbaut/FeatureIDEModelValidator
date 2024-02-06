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
  "deadFeatureExplanation": {
    "AffectedConstraints": {
      "value": "[AConstraint [propNode=GoalB => FeatureB], AConstraint [propNode=GoalC => FeatureC]]"
    },
    "AffectedElements": {
      "value": "[GoalA, FeatureB, FeatureC, GoalB, GoalC, AConstraint [propNode=GoalB => FeatureB], AConstraint [propNode=GoalC => FeatureC], Root]"
    },
    "ReasonCounts": {
      "value": "{FeatureModelReason[Root => GoalA]=1, FeatureModelReason[-(FeatureB & FeatureC)]=1, FeatureModelReason[GoalA => GoalB]=1, FeatureModelReason[GoalA => GoalC]=1, FeatureModelReason[GoalB => FeatureB]=1, FeatureModelReason[GoalC => FeatureC]=1}"
    },
    "AffectedFeatures": {
      "value": "[GoalA, FeatureB, FeatureC, GoalB, GoalC, Root]"
    },
    "ReasonCount": {
      "value": "6"
    },
    "ExplanationCount": {
      "value": "1"
    },
    "Reasons": {
      "value": "[FeatureModelReason[Root => GoalA], FeatureModelReason[-(FeatureB & FeatureC)], FeatureModelReason[GoalA => GoalB], FeatureModelReason[GoalA => GoalC], FeatureModelReason[GoalB => FeatureB], FeatureModelReason[GoalC => FeatureC]]"
    },
    "Class": {
      "value": "class de.ovgu.featureide.fm.core.explanations.fm.DeadFeatureExplanation"
    },
    "Void": {
      "value": "true"
    },
    "Implication": {
      "value": "-Root"
    },
    "Writer": {
      "Symbols": [
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {}
      ],
      "ReasonsString": "\n• GoalA is a mandatory child of Root (i.e., Root ⇒ GoalA).\n• FeatureB and FeatureC are alternatives (i.e., ¬(FeatureB ∧ FeatureC)).\n• GoalB is a mandatory child of GoalA (i.e., GoalA ⇒ GoalB).\n• GoalC is a mandatory child of GoalA (i.e., GoalA ⇒ GoalC).\n• GoalB ⇒ FeatureB is a constraint.\n• GoalC ⇒ FeatureC is a constraint.",
      "HeaderString": "The feature model is void because:",
      "String": "The feature model is void because:\n• GoalA is a mandatory child of Root (i.e., Root ⇒ GoalA).\n• FeatureB and FeatureC are alternatives (i.e., ¬(FeatureB ∧ FeatureC)).\n• GoalB is a mandatory child of GoalA (i.e., GoalA ⇒ GoalB).\n• GoalC is a mandatory child of GoalA (i.e., GoalA ⇒ GoalC).\n• GoalB ⇒ FeatureB is a constraint.\n• GoalC ⇒ FeatureC is a constraint.",
      "CircumstanceString": "The feature model is void"
    },
    "Subject": {
      "Structure": {
        "FirstChild": {
          "FirstChild": {
            "Feature": {
              "InternalId": {
                "value": "2"
              },
              "Property": {
                "DisplayName": "FeatureB"
              },
              "Name": "FeatureB"
            }
          },
          "LastChild": {
            "Feature": {
              "InternalId": {
                "value": "3"
              },
              "Property": {
                "DisplayName": "FeatureC"
              },
              "Name": "FeatureC"
            }
          },
          "Children": {
            "value": "[FeatureStructure=(FeatureB, mandatory=false), FeatureStructure=(FeatureC, mandatory=false)]"
          },
          "Feature": {
            "InternalId": {
              "value": "1"
            },
            "Property": {
              "DisplayName": "FeatureA"
            },
            "Name": "FeatureA"
          }
        },
        "LastChild": {
          "FirstChild": {
            "RelevantConstraints": {
              "value": "[AConstraint [propNode=GoalB => FeatureB]]"
            },
            "Feature": {
              "InternalId": {
                "value": "5"
              },
              "Property": {
                "DisplayName": "GoalB"
              },
              "Name": "GoalB"
            }
          },
          "LastChild": {
            "Class": {
              "value": "class de.ovgu.featureide.fm.core.base.impl.FeatureStructure"
            },
            "Children": {
              "value": "[]"
            },
            "RelevantConstraints": {
              "value": "[AConstraint [propNode=GoalC => FeatureC]]"
            },
            "Feature": {
              "InternalId": {
                "value": "6"
              },
              "Class": {
                "value": "class de.ovgu.featureide.fm.core.base.impl.Feature"
              },
              "Property": {
                "DisplayName": "GoalC"
              },
              "FeatureModel": {
                "FeatureTable": {
                  "value": "{Root=Root, FeatureA=FeatureA, FeatureB=FeatureB, FeatureC=FeatureC, GoalA=GoalA, GoalB=GoalB, GoalC=GoalC}"
                },
                "NextElementId": {
                  "value": "9"
                },
                "FeatureOrderList": {
                  "value": "[Root, FeatureA, FeatureB, FeatureC, GoalA, GoalB, GoalC]"
                },
                "ConstraintCount": {
                  "value": "2"
                },
                "NumberOfFeatures": {
                  "value": "7"
                },
                "FactoryID": "de.ovgu.featureide.fm.core.DefaultFeatureModelFactory",
                "Constraints": {
                  "value": "[AConstraint [propNode=GoalB => FeatureB], AConstraint [propNode=GoalC => FeatureC]]"
                },
                "RenamingsManager": {
                  "OldFeatureNames": {
                    "value": "[GoalA, GoalB, Root, FeatureC, FeatureB, FeatureA, GoalC]"
                  },
                  "Class": {
                    "value": "class de.ovgu.featureide.fm.core.RenamingsManager"
                  }
                },
                "Features": {
                  "value": "[Root, FeatureA, FeatureB, FeatureC, GoalA, GoalB, GoalC]"
                },
                "VisibleFeatures": {
                  "value": "[Root, FeatureA, FeatureB, FeatureC, GoalA, GoalB, GoalC]"
                },
                "Class": {
                  "value": "class de.ovgu.featureide.fm.core.base.impl.FeatureModel"
                },
                "Id": {
                  "value": "0"
                },
                "Structure": {
                  "FeaturesPreorder": {
                    "value": "[Root, FeatureA, FeatureB, FeatureC, GoalA, GoalB, GoalC]"
                  },
                  "Class": {
                    "value": "class de.ovgu.featureide.fm.core.base.impl.FeatureModelStructure"
                  }
                },
                "Property": {
                  "Class": {
                    "value": "class de.ovgu.featureide.fm.core.base.impl.FeatureModelProperty"
                  }
                }
              },
              "Name": "GoalC",
              "CustomProperties": {
                "Class": {
                  "value": "class de.ovgu.featureide.fm.core.base.impl.MapPropertyContainer"
                },
                "Properties": {
                  "value": "[]"
                }
              }
            },
            "ChildrenCount": {
              "value": "0"
            }
          },
          "Children": {
            "value": "[FeatureStructure=(GoalB, mandatory=true), FeatureStructure=(GoalC, mandatory=true)]"
          },
          "Feature": {
            "InternalId": {
              "value": "4"
            },
            "Property": {
              "DisplayName": "GoalA"
            },
            "Name": "GoalA"
          }
        },
        "Children": {
          "value": "[FeatureStructure=(FeatureA, mandatory=true  alt[FeatureB, mandatory=false, FeatureC, mandatory=false]), FeatureStructure=(GoalA, mandatory=true  and[GoalB, mandatory=true, GoalC, mandatory=true])]"
        }
      },
      "Property": {
        "DisplayName": "Root",
        "Class": {
          "value": "class de.ovgu.featureide.fm.core.base.impl.FeatureProperty"
        },
        "Implicit": {
          "value": "false"
        }
      },
      "Name": "Root",
      "CustomProperties": {
        "Properties": {
          "value": "[Entry [key=collapsed, type=graphics, value=false]]"
        }
      }
    }
  },
  "hasFalseOptionalFeatures": false,
  "hasVoidModelConstraints": true,
  "hasIndeterminateHiddenFeatures": false
}
```

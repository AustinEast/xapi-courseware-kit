# Courseware Instrumentation with xAPI

## Description

This document represents the Riptide Elements® implementation of xAPI. This library demonstrates many of the generic statements used in our courseware.

In this document we will refer to concepts such as: _activity_, _page_ and _topic_. These ideas relate specifically to how the Elements e-learning software is setup. In Elements, a single course is made up of one or more _topics_. Furthermore, each _topic_ is comprised of one or more _pages_. An _activity_ is an interactive section of a course (such as a drag-and-drop exercise) usually on a single _page_. Below is an example skeleton of a traditional course:

```
└─┬ Course
  ├─┬ Topic
  │ ├── Page
  │ ├─┬ Page
  │ │ └── Activity (Drag-And-Drop)
  │ └── Page
  └─┬ Topic
    ├── Page
    ├─┬ Page
    │ └── Activity (Multiple Choice Assessment)
    ├─┬ Page
    │ └── Activity (Multiple Choice Assessment)
    └─┬ Page
      └── Activity (Assessment Results)
```

Generated statements fall into two basic categories: Course level (can also be refered to as App level) and Activity level statements. Course level statements are more general and cover the majority of generic actions a user can take. Activity level statements are more specific to the various activities that users will interact with.

# Statement Generators

At Riptide Elements®, we used statement generating functions that take in contextual information from courses and use that to create valid statements that are then sent to an LRS. 

The following statement generating functions have been seperated out by whether they generate Course level or Activity level statements. Within those catagories, they have been organized into sections based on what information the statements are tracking (e.g. video-based statements, question-based statements).

## Table of Contents


- [Course Level Statements](#course-level-statements)
  * [Course](#course)
    + [onCourseLaunched](#oncourselaunched)
    + [onCourseInitialized](#oncourseinitialized)
    + [onCourseTerminated](#oncourseterminated)
    + [onCourseCompleted](#oncoursecompleted)
    + [Course Statement Example](#course-statement-example)
  * [Topic](#topic)
    + [onTopicLaunched](#ontopiclaunched)
    + [onTopicComplete](#ontopiccomplete)
    + [Topic Statement Example](#topic-statement-example)
  * [Page](#page)
    + [onPageLaunched](#onpagelaunched)
    + [onPageLeft](#onpageleft)
    + [onPageCompleted](#onpagecompleted)
    + [Page Statement Example](#page-statement-example)
- [Activity Level Statements](#activity-level-statements)
  * [Activity](#activity)
    + [onActivityLaunched](#onactivitylaunched)
    + [onActivityCompleted](#onactivitycompleted)
    + [Activity Statement Example](#activity-statement-example)
  * [Assessments](#assessments)
    + [onAssessmentLaunched](#onassessmentlaunched)
    + [onAssessmentInitialized](#onassessmentinitialized)
    + [onAssessmentAttempted](#onassessmentattempted)
    + [onAssessmentPassed](#onassessmentpassed)
    + [onAssessmentFailed](#onassessmentfailed)
    + [onAssessmentCompleted](#onassessmentcompleted)
    + [onAssessmentTerminated](#onassessmentterminated)
    + [Assessment Statement Example](#assessment-statement-example)
  * [Branching](#branching)
    + [onBranchingSimulationLaunched](#onbranchingsimulationlaunched)
    + [onBranchingSimulationProgressed](#onbranchingsimulationprogressed)
    + [onBranchingSimulationCompleted](#onbranchingsimulationcompleted)
    + [onBranchingSimulationAttempted](#onbranchingsimulationattempted)
    + [onBranchingSimulationMastered](#onbranchingsimulationmastered)
    + [Branching Statement Example](#branching-statement-example)
  * [Questions](#questions)
    + [onAnswerChanged](#onanswerchanged)
    + [onQuestionAsked](#onquestionasked)
    + [onQuestionAnswered](#onquestionanswered)
    + [Question Statement Example](#question-statement-example)
  * [Tooltips](#tooltips)
    + [toolTipsInitialized](#tooltipsinitialized)
    + [toolTipTouched](#tooltiptouched)
    + [toolTipsCompleted](#tooltipscompleted)
    + [ToolTips Statement Example](#tooltips-statement-example)
  * [Videos](#videos)
    + [onVideoSeeked](#onvideoseeked)
    + [onVideoPlayed](#onvideoplayed)
    + [onVideoPaused](#onvideopaused)
    + [onVideoEnded](#onvideoended)
    + [Video Statement Example](#video-statement-example)
  * [Other](#other)
    + [onFreeResponseAnswered](#onfreeresponseanswered)
- [Extending Statements](#extending-statements)
    + [addExtension](#addextension)

## Course Level Statements

### Course

These statements hold information on a user's progress through a course. Analyzing these statements can provide some important insights including: which users have completed the course, how long the entire course takes to complete, and even a particular user's progress percentage. These statements do not require extra contextual data to function.

#### onCourseLaunched

Used to generate a statement each time the system starts up the course for a user.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**N/A** | _{N/A}_ | N/A


#### onCourseInitialized

Used to generate a statement each time the system starts up the course for a new user (users first time in course).

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [INITIALIZED](http://www.adlnet.gov/expapi/verbs/initialized.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**N/A** | _{N/A}_ | N/A

#### onCourseTerminated

Used to generate a statement each time the system closes the learning session.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [TERMINATED](http://www.adlnet.gov/expapi/verbs/terminated.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**N/A** | _{N/A}_ | N/A


#### onCourseCompleted

Used to generate a statement each time the system closes the learning session.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|-----------
**N/A** | _{N/A}_ | N/A


#### Course Statement Example

Completing a course could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:sjoyce@gmail.com",
        "name": "Susan Joyce"
      },
      "verb": {
        "id": "http://www.adlnet.gov/expapi/verbs/completed.html",
        "display": {
          "en-US": "completed"
        }
      },
       "object": {
        "id": "http://elmnts.com/courses/demo",
        "objectType": "Activity",
        "definition": {
          "name": {
            "en-us": "Demo Subject"
          },
          "description": {
            "en-us": "N/A"
          },
          "type": "http://adlnet.gov/expapi/activities/course.html"
        }
      },
      "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "extensions": {
          "http://elmnts.com/courseware/pageId": "19",
          "http://elmnts.com/courseware/topicId": "3"
        }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Topic

These statements hold information on a user's progress through topics.

#### onTopicLaunched

Used to generate a statement each time the a user launches a page.

> ACTIVITY: [MODULE](http://www.adlnet.gov/expapi/activities/module.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**url** | _{string}_ | Url of Launched Page

#### onTopicComplete

Used to generate a statement each time the a user launches a page.

> ACTIVITY: [MODULE](http://www.adlnet.gov/expapi/activities/module.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**url** | _{string}_ | Url of Launched Page

#### Topic Statement Example

Completing a topic could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        	"mbox": "mailto:providerDefault@noreply.com",
        	"name": "provider Default"
    	},
    	"verb": {
        	"id": "http://adlnet.gov/expapi/verbs/completed",
        	"display": {
            	"en-us": "completed"
        	}
    	},
    	"object": {
        	"id": "https://elmnts.com/organizations/www/courses/test/topics/test",
	        "objectType": "Activity",
	        "definition": {
	            "name": {
	                "en-us": "mock topic"
	            },
	            "description": {
	                "en-us": "mock course - mock topic"
	            }
	        }
	    },
	    "result": {
	        "completion": true,
	        "extensions": {
	            "https://elmnts.com/courseware/topic/count": 2
	        }
	    },
	    "context": {
	        "registration": "00000000-a000-4000-a000-000000000000",
	        "revision": "Elements",
	        "language": "en-us",
	        "extensions": {
	            "https://elmnts.com/organization/user/attribute/team": "ExampleTeam",
	            "https://elmnts.com/organization/user/attribute/base": "Castillo De San Marcos",
	            "https://elmnts.com/organization/user/attribute/country": "USA",
	            "https://elmnts.com/courseware/pageName": "Page Two",
	            "https://elmnts.com/courseware/pageId": "2",
	            "https://elmnts.com/courseware/topicName": "test",
	            "https://elmnts.com/courseware/topicId": 1
	        }
    	},
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Page

These statements hold information on a user's progress through individual pages.

#### onPageLaunched

Used to generate a statement each time a user launches a page.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**url** | _{string}_ | Url of Launched Page


#### onPageLeft

Used to generate a statement each time a user leaves a page.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [PROGRESSED](http://www.adlnet.gov/expapi/verbs/progressed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name

#### onPageCompleted

Used to generate a statement each time the system closes the learning session.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|-----------
**N/A** | _{N/A}_ | N/A


#### Page Statement Example

Launching a page with the data:

```javascript
    var contextualData = {
        "url": "www.example.com"
    }
```
could result in the corresponding xAPI statement:

```json
    {
    "actor": {
        "mbox": "mailto:sjoyce@gmail.com",
        "name": "Susan Joyce"
    },
    "verb": {
        "id": "http://adlnet.gov/expapi/verbs/launched",
        "display": {
            "en-us": "launched"
        }
    },
    "object": {
        "id": "http://elmnts.com/courses/demo",
        "objectType": "Activity",
        "definition": {
            "name": {
                "en-us": "Demo Page"
            },
            "description": {
                "en-us": "N/A"
            }
        }
    },
    "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "revision": "Elements",
        "language": "en-us",
        "extensions": {
            "https://elmnts.com/courseware/pageId": "1",
            "https://elmnts.com/courseware/topicId": 12
        }
    },
    "timestamp": "2017-04-03T20:18:48.004Z"
}
```

## Activity Level Statements

### Activity
These statements hold information on a user's progress through Activities.

#### onActivityLaunched

Used to generate a statement each time an activity is launched.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activityName** | _{string}_ | Associated Activity Name

#### onActivityCompleted

Used to generate a statement when an activity is marked as complete.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activityID** | _{number}_ | Associated Activity ID
**resultsPresent** | _{boolean}_ | Should Activity Results Be Appended
**success** | _{boolean}_ | User's Success in Activity
**min** | _{number}_ | Lowest Possible Score
**max** | _{number}_ | Maximum Possible Score
**score** | _{number}_ | User's Earned Score

#### Activity Statement Example

Launching an Activity could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
          "mbox": "mailto:providerDefault@noreply.com",
          "name": "provider Default"
      },
      "verb": {
          "id": "http://adlnet.gov/expapi/verbs/launched",
          "display": {
              "en-us": "launched"
          }
      },
      "object": {
          "id": "https://elmnts.com/organizations/www/courses/test/topics/test/pages/2/activities/Matching",
          "objectType": "Activity",
          "definition": {
              "name": {
                  "en-us": "Matching"
              },
              "description": {
                  "en-us": "mock course - mock topic - 2 - Matching"
              },
              "type": "http://adlnet.gov/expapi/activities/simulation"
          }
      },
      "context": {
          "registration": "00000000-a000-4000-a000-000000000000",
          "revision": "Elements",
          "language": "en-us",
          "extensions": {
              "https://elmnts.com/organization/user/attribute/team": "ExampleTeam",
              "https://elmnts.com/organization/user/attribute/base": "Castillo De San Marcos",
              "https://elmnts.com/organization/user/attribute/country": "USA",
              "https://elmnts.com/courseware/pageName": "Page Two",
              "https://elmnts.com/courseware/pageId": "2",
              "https://elmnts.com/courseware/topicName": "test",
              "https://elmnts.com/courseware/topicId": 1
          }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Assessments

Assessments are activities with questions for the user to answer.

#### onAssessmentLaunched

Used to generate a statement each time an assessment is started.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID

#### onAssessmentInitialized

Used to generate a statement when formal tracking of the assessment starts.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [INITIALIZED](http://www.adlnet.gov/expapi/verbs/initialized.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID

#### onAssessmentAttempted

Used to generate a statement each time a user finishes all required sections of an activity, regardless of level of success.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [ATTEMPTED](http://www.adlnet.gov/expapi/verbs/attempted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID

#### onAssessmentPassed

Used to generate a statement when a user has passed the given assessment.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [PASSED](http://www.adlnet.gov/expapi/verbs/passed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID
**resultsPresent** | _{boolean}_ | Should Assessment Results Be Appended
**success** | _{boolean}_ | User's Success in Assessment
**min** | _{number}_ | Lowest Possible Score
**max** | _{number}_ | Maximum Possible Score
**score** | _{number}_ | User's Earned Score

#### onAssessmentFailed

Used to generate a statement when a user has failed the given assessment.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [FAILED](http://www.adlnet.gov/expapi/verbs/failed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID
**resultsPresent** | _{boolean}_ | Should Assessment Results Be Appended
**success** | _{boolean}_ | User's Success in Assessment
**min** | _{number}_ | Lowest Possible Score
**max** | _{number}_ | Maximum Possible Score
**score** | _{number}_ | User's Earned Score

#### onAssessmentCompleted

Used to generate a statement each time a user finishes all required sections of an activity with a satisfying level of success.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID

#### onAssessmentTerminated

Used to generate a statement when formal tracking of the assessment ends.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [TERMINATED](http://www.adlnet.gov/expapi/verbs/terminated.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**assessmentID** | _{number}_ | Associated Assessment ID

#### Assessment Statement Example

Attempting a course with the data:

```javascript
    var contextualData = {
        "activityID": "0",
   }
```
could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:tleonhardt@gmail.com",
        "name": "Tyler Leonhardt"
      },
      "verb": {
        "id": "http://www.adlnet.gov/expapi/verbs/attempted.html",
        "display": {
          "en-us": "attempted"
        }
      },
      "object": {
        "id": "http://elmnts.com/courseware/cvit/BuildingOnIt/12",
        "objectType": "Activity",
        "definition": {
          "type": "http://www.adlnet.gov/expapi/activities/assessment.html"
        }
      },
      "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "extensions": {
          "http://elmnts.com/courseware/pageId": "12",
          "http://elmnts.com/courseware/topicId": "3"
        }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```
### Branching

Branching activities are activities that offer multiple paths to completion.

#### onBranchingSimulationLaunched

Used to generate a statement when a branching activity is launched.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**name** | _{string}_ | Name of Current Branching Activity
**description** | _{string}_ | Description of Current Branching Activity
**activityName** | _{string}_ | Name of Active Activity

#### onBranchingSimulationProgressed

Used to generate a statement when a user progresses through a branching activity.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [progressed](http://www.adlnet.gov/expapi/verbs/progressed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**name** | _{string}_ | Name of Current Branching Activity
**description** | _{string}_ | Description of Current Branching Activity
**activityName** | _{string}_ | Name of Active Activity

#### onBranchingSimulationCompleted

Used to generate a statement when a branching activity is completed.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**name** | _{string}_ | Name of Current Branching Activity
**description** | _{string}_ | Description of Current Branching Activity
**activityName** | _{string}_ | Name of Active Activity
**score** | _{number}_ | User's Raw Score for Activity
**min** | _{number}_ | Minimum Points Available for Activity
**possible** | _{number}_ | Maximum Points Available for Activity
**success** | _{boolean}_ | Simulation success threshold reached

#### onBranchingSimulationAttempted

Used to generate a statement when a branching activity is completed.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**name** | _{string}_ | Name of Current Branching Activity
**description** | _{string}_ | Description of Current Branching Activity
**activityName** | _{string}_ | Name of Active Activity
**score** | _{number}_ | User's Raw Score for Activity
**min** | _{number}_ | Minimum Points Available for Activity
**possible** | _{number}_ | Maximum Points Available for Activity
**success** | _{boolean}_ | Simulation success threshold reached

#### onBranchingSimulationMastered

Used to generate a statement when the final branching activity is completed.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**name** | _{string}_ | Name of Current Branching Activity
**description** | _{string}_ | Description of Current Branching Activity
**activityName** | _{string}_ | Name of Active Activity
**score** | _{number}_ | User's Raw Score for Activity
**possible** | _{number}_ | Maximum Points Available for Activity
**success** | _{boolean}_ | Simulation success threshold reached
**completed** | _{boolean}_ | Value Determining User's Completion

#### Branching Statement Example

Progressing a Branching Activity could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
	       "mbox": "mailto:providerDefault@noreply.com",
	       "name": "provider Default"
	   },
	   "verb": {
	   		"id": "http://adlnet.gov/expapi/verbs/progressed",
	    	"display": {
	           "en-us": "progressed"
	       }
	   },
	   "object": {
	       "id": "https://elmnts.com/organizations/www/courses/test/topics/test/pages/2/activities/ComplexBranching",
	       "objectType": "Activity",
	       "definition": {
	           "name": {
	               "en-us": "Flight Attendent Etiquette"
	           },
            	 "description": {
              	"en-us": "An example of an exchange between flight attendant and pasenger"
	           },
	           "type": "http://adlnet.gov/expapi/activities/simulation"
	       }
	   },
	   "context": {
	       "registration": "00000000-a000-4000-a000-000000000000",
	       "revision": "Elements",
	       "language": "en-us",
	       "extensions": {
	           "https://elmnts.com/courseware/pageId": "2",
	           "https://elmnts.com/courseware/topicId": 1,
	           "https://elmnts.com/user/attribute/exampleAttr": 5000
	       }
	   },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Questions

Questions may consist of: Knowledge Check, Survey, Feedback Responses, etc. Additionally Questions are used inside many other activity types.


#### onAnswerChanged

Used to generate a statement each time a user changes his/her answer choice, clicks/touches related interactive question media.

> ACTIVITY: [INTERACTION](http://www.adlnet.gov/expapi/activities/interaction.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**givenAnswer** | _{array}_ | Currently Selected Answer(s)

#### onQuestionAsked

Used to generate a statement each time the system displays an unanswered question.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [ASKED](http://www.adlnet.gov/expapi/verbs/asked.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)


#### onQuestionAnswered

Used to generate a statement each a user submits a question for grading.

> ACTIVITY: [INTERACTED](http://www.adlnet.gov/expapi/activities/interacted.html)
> VERB: [ANSWERED](http://www.adlnet.gov/expapi/verbs/answered.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**givenAnswer** | _{array}_ | User's Answer Choice(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**orderMatters** | _{boolean}_ | Should Order Determine Correctness

#### Question Statement Example

Asking a question with the data:

```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "3",
        "activity": "BodyInTheCrowd",
        "questionId": "28",
        "questionText": "What is the Most Likely reason why Person 3 displayed little interest when the clerk was being yelled at?",
        "correctAnswer": ["b"],
        "possibleAnswers": {
            "a": "He is shoplifting and doesn’t want to be noticed.",
            "b": "He knows one of the people involved and doesn’t want to get involved, himself.",
            "c": "He was waiting to detonate an explosive and now missed out on his chance.",
            "d": "He doesn’t like confrontation."
        }
    }
```
could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:mjoyce@gmail.com",
        "name": "Michael Joyce"
      },
      "verb": {
        "id": "http://adlnet.gov/expapi/verbs/asked",
        "display": {
          "en-us": "asked"
        }
      },
      "object": {
        "id": "http://elmnts.com/courseware/cvit/kinesics/8/qid/28",
        "objectType": "Activity",
        "definition": {
          "name": {
            "en-us": "BodyInTheCrowd"
          },
          "description": {
            "en-us": "What is the Most Likely reason why Person 3 displayed little interest when the clerk was being yelled at?"
          }
        }
      },
      "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "extensions": {
          "http://elmnts.com/courseware/pageId": "3",
          "http://elmnts.com/courseware/topicId": "3"
        }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Tooltips

Tooltips are activities that require user input to relay supplementary information on a topic.

#### toolTipsInitialized

Used to generate a statement when a Tooltip activity is launched.

> ACTIVITY: [TOOLTIP](http://www.adlnet.gov/expapi/activities/tooltip.html)
> VERB: [INITIALIZED](http://www.adlnet.gov/expapi/verbs/initialized.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**tooltipId** | _{string}_ | Unique Tooltip ID

#### toolTipTouched

Used to generate a statement when a tooltip is interacted with.

> ACTIVITY: [TOOLTIP](http://www.adlnet.gov/expapi/activities/tooltip.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**tooltipId** | _{string}_ | Unique Tooltip ID

#### toolTipsCompleted

Used to generate a statement when all tooltips in an activity have been interacted with.

> ACTIVITY: [TOOLTIP](http://www.adlnet.gov/expapi/activities/tooltip.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**tooltipId** | _{string}_ | Unique Tooltip ID

#### ToolTips Statement Example

Initializing a Tooltip could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
       	"account": {
           	"homePage": "https://www.elmnts.com/organizations/www",
           	"name": "00000000-a000-4000-a000-000000000000"
      		 }
   		},
    	"verb": {
       	"id": "http://adlnet.gov/expapi/verbs/initialized",
       	"display": {
          	 "en-us": "initialized"
       	}
    	},
    	"object": {
       	"id": "https://elmnts.com/organizations/www/courses/test/topics/test/pages/2/tooltips",
        	"objectType": "Activity",
	        	"definition": {
		           "type": "http://adlnet.gov/expapi/activities/tooltip",
		           "extensions": {
		                "https://elmnts.com/courseware/activityExtensions/videoSrc": [
		                  "path/to/video.mp4"
		              ],
		                "https://elmnts.com/courseware/activityExtensions/callbackTime": "11",
		                "https://elmnts.com/courseware/activityExtensions/allTooltipIds": [
		                  "id1",
		                  "id2",
		                  "id3"
		              ]
		           }
		        }
		     }
        }
    },
    "context": {
        "registration": "00000000-a000-4000-a000-000000000000",
        "revision": "Elements",
        "language": "en-us",
        "extensions": {
            "https://elmnts.com/courseware/pageId": "2",
            "https://elmnts.com/courseware/topicId": "1",
            "https://elmnts.com/user/attribute/exampleAttr": 5000
        }
    },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Videos

These statements hold information about a user's interaction with video content. With this information, you determine trends such as: what sections users rewatch, pause at, keep muted, or skip through.

#### onVideoSeeked

Used to generate a statement when a user seeks through a video.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**src** | _{string}_ | Source File For Video
**previousTime** | _{number}_ | Point In Video Before Interaction
**currentTime** | _{number}_ | Point In Video After Interaction
**volume** | _{number}_ | Current Volume Of Video
**duration** | _{number}_ | Total Duration Of Video

#### onVideoPlayed

Used to generate a statement when a user plays a video.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**src** | _{string}_ | Source File For Video
**currentTime** | _{number}_ | Point In Video After Interaction
**volume** | _{number}_ | Current Volume Of Video

#### onVideoPaused

Used to generate a statement when a user pauses a video.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**src** | _{string}_ | Source File For Video
**currentTime** | _{number}_ | Point In Video After Interaction
**volume** | _{number}_ | Current Volume Of Video

#### onVideoEnded

Used to generate a statement when a user finishes video.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**src** | _{string}_ | Source File For Video
**volume** | _{number}_ | Current Volume Of Video
**duration** | _{number}_ | Total Duration Of Video

#### Video Statement Example

Seeking a Video could result in the corresponding xAPI statement:

```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
          "mbox": "mailto:providerDefault@noreply.com",
          "name": "provider Default"
      },
      "verb": {
      	   "id": "http://adlnet.gov/expapi/verbs/interacted",
       	"display": {
              "en-us": "interacted"
          }
      },
      "object": {
          "id": "https://elmnts.com/organizations/www/courses/test/media/src/example.mp4",
          "objectType": "Activity",
          "definition": {
              "name": {
                  "en-us": "topics/3/video/example.mp4"
              },
              "type": "http://adlnet.gov/expapi/activities/media"
          }
      },
      "context": {
          "registration": "00000000-a000-4000-a000-000000000000",
          "revision": "Elements",
          "language": "en-us",
          "extensions": {
              "https://elmnts.com/courseware/video/interaction": "seeked",
              "https://elmnts.com/courseware/video/previousTime": "18000",
              "https://elmnts.com/courseware/video/currentTime": "14500",
              "https://elmnts.com/courseware/video/volume": ".5",
              "https://elmnts.com/courseware/video/duration": "20000",
              "https://elmnts.com/courseware/pageId": "2",
              "https://elmnts.com/courseware/topicId": "1",
              "https://elmnts.com/user/attribute/exampleAttr": 5000
          }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```

### Other

#### onFreeResponseAnswered

Used to generate a statement when the user a commits a free response question.

> ACTIVITY: [INTERACTION](http://www.adlnet.gov/expapi/activities/interaction.html)
> VERB: [ANSWERED](http://www.adlnet.gov/expapi/verbs/answered.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activityName** | _{string}_ | Name of Active Activity
**questionText** | _{string}_ | Question Text
**questionId** | _{number}_ | Unique Question Id
**disclosure** | _{string}_ | User Entered Free Response

## Extending Statements

The Elements Platform has the ability to extend statements. Here's a quick glance at how we add additional extensions to an xAPI Statement.

#### addExtension

Here's how you could create a media experienced statement with an video-specific extension:

```javascript
    var extensions = {
      "activity": {
        "http://elmnts.com/courseware/video/duration": 30.647,
        "http://elmnts.com/courseware/video/interaction": "seeked",
        "http://elmnts.com/courseware/video/volume": 0.75,
        "http://elmnts.com/courseware/video/previousTime": 30.647
      }
    };
    var extendedStatement = onMediaExperienced(statementData).addExtension(extensions);
```



For more information on xAPI statements, visit [ADL's xAPI Vocabulary](http://www.adlnet.gov/expapi/index.html).

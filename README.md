# Courseware Instrumentation with xAPI

## Description

This document represents the Riptide Elements® implementation of xAPI. This library demonstrates many of the generic statements used in our courseware.

In this document we will refer to concepts such as: _activity_, _page_ and _topic_. These ideas relate specifically to how the Elements e-learning software is setup. In Elements, a single course is made up of one or more _topics_. Furthermore, each _topic_ is comprised of one or more _pages_. An _activity_ is an interactive section of a course (such as a drag-and-drop exercise) usually on a single _page_.

## Table of Contents
* [**Answers**](### Answers)
⋅⋅* [onAnswerChanged](#### onAnswerChanged())
⋅⋅* [Answer Statement Example](#### Answer Statement Example)
* [**Assessments**](### Assessments)
⋅⋅* [onAssessmentLaunched](#### onAssessmentLaunched())
⋅⋅* [onAssessmentAttempted](#### onAssessmentAttempted())
⋅⋅* [onAssessmentCompleted](#### onAssessmentCompleted())
⋅⋅* [Assessment Statement Example](#### Assessment Statement Example)
* [**Course**](### Course)
⋅⋅* [onCourseInitialized](#### onCourseInitialized())
⋅⋅* [onCourseResumed](#### onCourseResumed())
⋅⋅* [onCourseProgressed](#### onCourseProgressed())
⋅⋅* [onCourseSuspended](#### onCourseSuspended())
⋅⋅* [onCourseTerminated](#### onCourseTerminated())
⋅⋅* [onCourseCompleted](#### onCourseCompleted())
⋅⋅* [Course Statement Example](#### Course Statement Example)
* [**Media**](### Media)
⋅⋅* [onMediaExperienced](#### onMediaExperienced())
⋅⋅* [onMediaInteracted](#### onMediaInteracted())
⋅⋅* [Media Statement Example](#### Media Statement Example)
* [**Module**](### Module)
⋅⋅* [onModuleLaunched](#### onModuleLaunched())
⋅⋅* [onModuleProgressed](#### onModuleProgressed())
⋅⋅* [onModuleExperienced](#### onModuleExperienced())
⋅⋅* [Module Statement Example](#### Module Statement Example)
* [**Questions**](### Questions)
⋅⋅* [onSimulationLaunched](#### onSimulationLaunched())
⋅⋅* [onQuestionAsked](#### onQuestionAsked())
⋅⋅* [onQuestionAnswered](#### onQuestionAnswered())
⋅⋅* [onQuestionCompleted](#### onQuestionCompleted())
⋅⋅* [onQuestionExperienced](#### onQuestionExperienced())
⋅⋅* [Question Statement Example](#### Question Statement Example)
* [**Simulations**](### Simulations)
⋅⋅* [onQuestionInteracted](#### onQuestionInteracted())
⋅⋅* [onSimulationAttempted](#### onSimulationAttempted())
⋅⋅* [onSimulationProgressed](#### onSimulationProgressed())
⋅⋅* [onSimulationCompleted](#### onSimulationCompleted())
⋅⋅* [onSimulationMastered](#### onSimulationMastered())
⋅⋅* [Simulation Statement Example](#### Simulation Statement Example)
* [**Extending Statements**](### Extending Statements)
⋅⋅* [addExtension](#### addExtension())

### Answers

Answer statements are typically associated with user submitted questions.

#### onAnswerChanged()

Used to generate a statement each time a user changes his/her answer choice.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**givenAnswer** | _{array}_ | User's Answer Choice(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### Answer Statement Example

Changing an answer with the data:
```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "12",
        "activity": "KnowledgeCheck",
        "questionId": "3",
        "questionText": "Who warrants further observation because they could be a potential threat?"
        "givenAnswer": "b",
        "possibleAnswers": {
            "a":"Person 1",
            "b":"Person 2",
            "c":"Person 3",
            "d":"Person 4"
        },
        "correctAnswer": ["c"]
    }
```
could result in the corresponding xAPI statement:
```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:mgutkin@gmail.com",
        "name": "Matt Gutkin"
      },
      "verb": {
        "id": "http://www.adlnet.gov/expapi/verbs/interacted.html",
        "display": {
          "en-us": "interacted"
        }
      },
      "object": {
        "id": "http://elmnts.com/courseware/cvit/qid/3",
        "objectType": "Activity",
        "definition": {
          "name": {
            "en-us": "Question 3"
          },
          "description": {
            "en-us": "Who warrants further observation because they could be a potential threat?"
          },
          "type": "http://www.adlnet.gov/expapi/activities/question.html"
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


### Assessments

> Assessments are activities with questions.

#### onAssessmentLaunched()

Used to generate a statement each time an assessment is started.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**description** | _{string}_ | Description of Assessment


#### onAssessmentAttempted()

Used to generate a statement each time a user finishes all required sections of an activity, regardless of level of success.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [ATTEMPTED](http://www.adlnet.gov/expapi/verbs/attempted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**description** | _{string}_ | Description of Assessment


#### onAssessmentCompleted()

Used to generate a statement each time a user finishes all required sections of an activity with a satisfying level of success.

> ACTIVITY: [ASSESSMENT](http://www.adlnet.gov/expapi/activities/assessment.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**description** | _{string}_ | Description of Assessment
**score** | _{number}_ | User's Raw Score on Assessment


### Assessment Statement Example

Attempting a course with the data:
```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "12",
        "activity": "BuildingOnIt",
        "description": "Use the clues given to determine what the subject of the photos are."
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


### Course

> These statements hold information on a user's progress through a course. Analyzing these statements can provide some important insights including: which users have completed the course, how long the entire course takes to complete, and even a particular user's progress percentage.

#### onCourseInitialized()

Used to generate a statement each time the system starts up the course for a new user (users first time in course).

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [INITIALIZED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onCourseResumed()

Used to generate a statement each time the system starts up the course for a given user except for the very first time.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [RESUMED](http://www.adlnet.gov/expapi/verbs/resumed.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onCourseProgressed()

Used to generate a statement each time the user advances through the course.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [PROGRESSED](http://www.adlnet.gov/expapi/verbs/resumed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onCourseSuspended()

Used to generate a statement each time the system is _suspended_.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [TERMINATED](http://www.adlnet.gov/expapi/verbs/resumed.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onCourseTerminated()

Used to generate a statement each time the system closes the learning session.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [TERMINATED](http://www.adlnet.gov/expapi/verbs/resumed.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onCourseCompleted()

Used to generate a statement each time the system closes the learning session.

> ACTIVITY: [COURSE](http://www.adlnet.gov/expapi/activities/course.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|-----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


### Course Statement Example

Completing a course with the data:
```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "19",
    }
```
could result in the corresponding xAPI statement:
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


### Media

Media statements are those which involve interaction with videos, images, and animations.

#### onMediaExperienced()

Used to generate a statement each time a user views a page containing media.

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [EXPERIENCED](http://www.adlnet.gov/expapi/verbs/experienced.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**mediaSrc** | _{string} | Path to Media Source
**description** | _{}_ | Description of Media
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onMediaInteracted()

Used to generate a statement each time a user interacts with a page's media. (Examples include: seeking/pausing a video, selecting an imagemap area, etc.)

> ACTIVITY: [MEDIA](http://www.adlnet.gov/expapi/activities/media.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**mediaSrc** | _{string} | Path to Media Source
**description** | _{}_ | Description of Media
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


### Media Statement Example

Seeking a video with the data:
```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "2",
        "activity": "Video",
        "mediaSrc": "videos/what_is_kinesics.mp4",
        "description": "Video to walk the learner through the basics of Kinesics."
    }
```
could result in the corresponding xAPI statement:
```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:lwarr@gmail.com",
        "name": "Elizabeth Warren"
      },
      "verb": {
        "id": "http://www.adlnet.gov/expapi/verbs/interacted.html",
        "display": {
          "en-US": "interacted"
        }
      },
      "object": {
        "id": "http://elmnts.com/courseware/media/src/videos/what_is_kinesics.mp4",
        "objectType": "Activity",
        "definition": {
          "name": {
            "en-us": "videos/what_is_kinesics.mp4"
          },
          "description": {
            "en-us": "Video to walk the learner through the basics of Kinesics."
          }
        },
        "type":"http://www.adlnet.gov/expapi/activities/media.html"
      },
      "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "extensions": {
          "http://elmnts.com/courseware/video/duration": 30.647,
          "http://elmnts.com/courseware/video/currentTime": 7.974425,
          "http://elmnts.com/courseware/video/interaction": "seeked",
          "http://elmnts.com/courseware/video/volume": 0.75,
          "http://elmnts.com/courseware/video/previousTime": 8.005165,
          "http://elmnts.com/courseware/pageId": "2",
          "http://elmnts.com/courseware/topicId": "3"
        }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```



### Module

Modules represent any given segment of an learning experience. In Elements, modules usually coorespond to single topics, but may be used for delimiting other portions of a course as well.

#### onModuleLaunched()

Used to generate a statement each time the system begins a module.

> ACTIVITY: [MODULE](http://www.adlnet.gov/expapi/activities/module.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onModuleProgressed()

Used to generate a statement each time a user advances through a module.

> ACTIVITY: [MODULE](http://www.adlnet.gov/expapi/activities/module.html)
> VERB: [PROGRESSED](http://www.adlnet.gov/expapi/verbs/progressed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name

#### onModuleExperienced()

Used to generate a statement each time a user finishes (or visits a previously completed) module.

> ACTIVITY: [MODULE](http://www.adlnet.gov/expapi/activities/module.html)
> VERB: [EXPERIENCED](http://www.adlnet.gov/expapi/verbs/experienced.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


### Module Statement Example

Launching a module with the data:
```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "1",
    }
```
could result in the corresponding xAPI statement:
```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:sharpd@gmail.com",
        "name": "Daniel Sharp"
      },
      "verb": {
        "id": "http://www.adlnet.gov/expapi/verbs/experienced.html",
        "display": {
          "en-us": "launched"
        }
      },
      "object": {
        "id": "http://elmnts.com/courseware/cvit/kinesics/1",
        "objectType": "Activity",
        "definition": {
          "name": {
            "en-us": "kinesics"
          },
          "description": {
            "en-us": "Course Topic 3: Kinesics"
          },
          "type": "http://www.adlnet.gov/expapi/activities/module.html"
        }
      }
      "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "extensions": {
          "http://elmnts.com/courseware/pageId": "1",
          "http://elmnts.com/courseware/topicId": "3"
        }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```



### Questions

Questions may consist of: Knowledge Check, Survey, Feedback Responses, etc. Additionally Questions are used inside many other activity types.


#### onQuestionInteracted()

Used to generate a statement each time a user changes his/her answer choice, clicks/touches related interactive question media.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [INTERACTED](http://www.adlnet.gov/expapi/verbs/interacted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


## onQuestionAsked()

Used to generate a statement each time the system displays an unanswered question.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [ASKED](http://www.adlnet.gov/expapi/verbs/asked.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onQuestionAnswered()

Used to generate a statement each a user submits a question for grading.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [ANSWERED](http://www.adlnet.gov/expapi/verbs/answered.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**givenAnswer** | _{array}_ | User's Answer Choice(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onQuestionCompleted()

Used to generate a statement each a user submits a question for grading.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**givenAnswer** | _{array}_ | User's Answer Choice(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


#### onQuestionExperienced()

Used to generate a statement each time a user views question previously answered.

> ACTIVITY: [QUESTION](http://www.adlnet.gov/expapi/activities/question.html)
> VERB: [EXPERIENCED](http://www.adlnet.gov/expapi/verbs/experienced.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**questionId** | _{string}_ | Unique Question Id
**questionText** | _{string}_ | Question Text
**correctAnswer** | _{array}_ | Questions Correct Answer(s)
**givenAnswer** | _{array}_ | User's Answer Choice(s)
**possibleAnswers** | _{object}_ | Question's Possible Answer(s)
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name


### Question Statement Example

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


### Simulations

> Simulations are activities containing many objectives, often spanning over several pages. Some example Simulations may be: Branching Scenarios, Decision Points, Involved Custom Activites, Video with Questions, etc.


#### onSimulationLaunched()

Used to generate a statement each time the system sets up/displays a simulation activity.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [LAUNCHED](http://www.adlnet.gov/expapi/verbs/launched.html)
> ACTOR: SYSTEM

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**name** | _{string}_ | Simulation Name
**description** | _{string}_ | Description of Simulation
**score** | _{number}_ | User's Raw Score on Assessment
**success** | _{boolean}_ | Simulation success threshold reached
**completion** | _{boolean}_ | Simulation requirements satisfied


#### onSimulationAttempted()

Used to generate a statement each time the user navigates to the simulation's end.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [ATTEMPTED](http://www.adlnet.gov/expapi/verbs/attempted.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**name** | _{string}_ | Simulation Name
**description** | _{string}_ | Description of Assessment
**score** | _{number}_ | User's Raw Score on Assessment
**success** | _{boolean}_ | Simulation success threshold reached
**completion** | _{boolean}_ | Simulation requirements satisfied

#### onSimulationProgressed()

Used to generate a statement each time a user advances through a simulation.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [PROGRESSED](http://www.adlnet.gov/expapi/verbs/progressed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**name** | _{string}_ | Given Name of the Simulation
**description** | _{string}_ | Description of Simulation
**score** | _{number}_ | User's Raw Score on Simulation
**success** | _{boolean}_ | Simulation success threshold reached
**completion** | _{boolean}_ | Simulation requirements satisfied

#### onSimulationCompleted()

Used to generate a statement each time a user finishes a simulation.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [COMPLETED](http://www.adlnet.gov/expapi/verbs/completed.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**name** | _{string}_ | Given Name of the Simulation
**description** | _{string}_ | Description of Simulation
**score** | _{number}_ | User's Raw Score on Simulation
**success** | _{boolean}_ | Simulation success threshold reached

#### onSimulationMastered()

Used to generate a statement when a user successfully completes and satisfies all simulation requirements.

> ACTIVITY: [SIMULATION](http://www.adlnet.gov/expapi/activities/simulation.html)
> VERB: [MASTERED](http://www.adlnet.gov/expapi/verbs/mastered.html)
> ACTOR: USER

Contextual Data | Type | Description
-----------|----------|----------
**activity** | _{string}_ | Associated Activity Name
**page** | _{string}_ | Associated Page Number
**topic** | _{string}_ | Associated Topic Name
**name** | _{string}_ | Given Name of the Simulation
**description** | _{string}_ | Description of Simulation
**score** | _{number}_ | User's Raw Score on Simulation

### Simulation Statement Example

Launching a simulation with the data:
```javascript
    var contextualData = {
        "topic": "kinesics",
        "page": "8",
        "activity": "DangerZone",
        "score": 0,
        "success": false,
        "completed": false,
        "name": "DangerZone",
        "description": "Use the provided information to determine the correct level of danger."
    }
```
could result in the corresponding xAPI statement:
```json
    {
      "id": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
      "actor": {
        "mbox": "mailto:sglancy@gmail.com",
        "name": "Scott Glancy"
      },
      "verb": {
        "id": "http://www.adlnet.gov/expapi/verbs/launched.html",
        "display": {
          "en-us": "launched"
        }
      },
      "object": {
        "id": "http://elmnts.com/courseware/cvit/kinesics/8/DangerZone",
        "objectType": "Activity",
        "definition": {
          "name": {
            "en-us": "DangerZone"
          },
          "description": {
            "en-us": "Use the provided information to determine the correct level of danger."
          }
        }
      },
      "result": {
        "score": {
          "scaled": 0,
          "raw": 0
        },
        "success": false,
        "completion": false
      },
      "context": {
        "registration": "xxxxxxx-xxxx-xxx-xxxx-xxxxxxx",
        "extensions": {
          "http://elmnts.com/courseware/pageId": "8",
          "http://elmnts.com/courseware/topicId": "3"
        }
      },
      "timestamp": "2015-04-20T14:10:43.563Z",
      "stored": "2015-04-20T14:10:13.992Z"
    }
```


### Extending Statements

The Elements Platform has the ability to extend statements. Here's a quick glance at how we add additional extensions to an xAPI Statement.

#### addExtension()

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

Word Validator
==============

WordValidator validates that the attribute value has a specific words count and checks this value against whitelist and blacklist.
It is a port of https://github.com/antonCPU/word-validator from Anton Yakushin from Yii 1 to Yii 2.

##Requirements

Tested in Yii 2.0.9.

##Installation

composer require thyseus/yii2-word-validator

##Usage

Add the following code to your model class rules() method

~~~
use app\components\WordValidator;

public function rules()
{
   return [
       //other validators...
       array('attributeName', WordValidator::className(), , /*add here needed rules*/),
   );
}

~~~

For example:

~~~
use app\components\WordValidator;

public function rules() {
  return [
    [['message'], WordValidator::className(),
    'min' => 2,
    'max' => 5,
    'whitelist' => array('please', 'test'),
    'blacklist' => array('restricted', 'email.*'), //could be a regular expression
    'messages'  => array(
        'max' => '{attribute} is too long (maximum is {max} words, but now it\'s {length})'
        ),
    ];
  ];
~~~

#### Validation rules
- **max** - the attribute should contain less (or equal) words count;
- **min** - minimum words count;
- **exact** - expected only this words count;
- **blacklist** - array of words that should not be in the attribute.
                There also could be a regular expression;
- **whitelist** - at least one of these words/expressions must be in the attribute.

#### Messages
Any default error message could be overridden using **messages** parameter.
All messages support {attribute} and {length} placeholders. Each validation
method adds it's value to a correspond (the same as a name) placeholder.
For **min** rule a message could be specified as:
~~~
[/*...*/
    'messages' => array(
        'min' => 'Your {attribute} is now has {length} words. But should be
             at least {min}'
    ),
],
~~~

Client side validation is supported.

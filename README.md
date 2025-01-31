# Facelivenessdetection

A real-time facial verification feature using Google ML Kit for liveliness detection. It ensures user interaction through smiling, blinking, and head movements. Features include face detection, dynamic feedback, a countdown timer, and customizable UI—ideal for secure authentication and anti-spoofing verification. 🚀

![image](https://github.com/user-attachments/assets/eb0ca715-27f8-4aa5-9e23-fd11825e8960)
![image](https://github.com/user-attachments/assets/5f6729b3-8ec8-4d2a-b728-bcbb299379ae)

'''dart
  Widget build(BuildContext context) {
    return FaceDetectorView(
        onSuccessValidation: (validated) {},
        onChildren: ({required countdown, required state, required hasFace}) {
          return [
            SizedBox(height: 20),
            Row(
                spacing: 10,
                crossAxisAlignment: CrossAxisAlignment.center,
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Image.asset('assets/face_verification_icon.png',
                      height: 30, width: 30),
                  Flexible(
                      child: AnimatedSize(
                          duration: Duration(milliseconds: 150),
                          child: Text(
                            hasFace ? 'User face found' : 'User face not found',
                            style: _textStyle.copyWith(
                                color: Colors.black,
                                fontWeight: FontWeight.w400,
                                fontSize: 12),
                          )))
                ]),
            SizedBox(height: 30),
            Text(getHintText(state),
                style: _textStyle.copyWith(
                    color: Colors.black,
                    fontWeight: FontWeight.w600,
                    fontSize: 20)),
            if (countdown > 0)
              Text.rich(
                textAlign: TextAlign.center,
                TextSpan(children: [
                  TextSpan(text: 'IN'),
                  TextSpan(text: '\n'),
                  TextSpan(
                      text: countdown.toString(),
                      style: _textStyle.copyWith(
                          color: Colors.black,
                          fontWeight: FontWeight.w600,
                          fontSize: 22))
                ]),
                style: _textStyle.copyWith(
                    color: Colors.black,
                    fontWeight: FontWeight.w600,
                    fontSize: 16),
              )
            else ...[SizedBox(height: 50), CupertinoActivityIndicator()]
          ];
        },
        onRulesetCompleted: (ruleset) {
          if (!_completedRuleset.contains(ruleset)) {
            _completedRuleset.add(ruleset);
          }
        });
  }

String getHintText(Rulesets state) {
  String hint_ = '';
  switch (state) {
    case Rulesets.smiling:
      hint_ = 'Please Smile';
      break;
    case Rulesets.blink:
      hint_ = 'Please Blink';
      break;
    case Rulesets.tiltUp:
      hint_ = 'Please Look Up';
      break;
    case Rulesets.tiltDown:
      hint_ = 'Please Look Down';
      break;
    case Rulesets.toLeft:
      hint_ = 'Please Look Left';
      break;
    case Rulesets.toRight:
      hint_ = 'Please Look Right';
      break;
  }
  return hint_;
}

'''

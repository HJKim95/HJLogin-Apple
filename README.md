# HJLogin-Apple

## Example

AppleLoginTest - ViewController를 통해 설정 예시를 확인해볼 수 있습니다.

## Requirements
Signing & Capabilites 에서 Sign in with Apple 을 추가해주세요.

## Installation

import AuthenticationServices 만 해주고
다음과 같이 코드를 작성해주시면 됩니다.
```ruby
fileprivate func setUpProviderLoginView() {
    let button = ASAuthorizationAppleIDButton()
    button.addTarget(self, action: #selector(handleAppleLogin), for: .touchUpInside)
    view.addSubview(button)
    button.center = view.center
}

@objc fileprivate func handleAppleLogin() {
    let request = ASAuthorizationAppleIDProvider().createRequest()
    request.requestedScopes = [.fullName, .email]
    let controller = ASAuthorizationController(authorizationRequests: [request])
    controller.delegate = self
    controller.presentationContextProvider = self
    controller.performRequests()
}

func presentationAnchor(for controller: ASAuthorizationController) -> ASPresentationAnchor {
    return self.view.window!
}

func authorizationController(controller: ASAuthorizationController, didCompleteWithAuthorization authorization: ASAuthorization) {
    if let credential = authorization.credential as? ASAuthorizationAppleIDCredential {
        let userIdentifier = credential.user
        let fullName = credential.fullName
        let email = credential.email
        print(userIdentifier, fullName, email, separator: "\n")
        UserDefaults.standard.set(userIdentifier, forKey: "appleUserId")
    }
}
```

## Author

HJKim95, 25ephipany@naver.com

## License

HJLogin-Apple is available under the MIT license. See the LICENSE file for more info.

import Foundation

final class LoginViewModel {
    // 실시간으로 달라지는 데이터를 감지
    var inputId: String? {
        didSet {
            validation()
        }
    }
    var inputPassword: String? {
        didSet {
            validation()
        }
    }
    
    private(set) var outputValid = false
    private(set) var outputValidationText = ""
    
    private func validation() {
        guard let id = inputId, let pw = inputPassword else { return }
        
        if id.count >= 3 && pw.count > 5 {
            print("유효성 통과")
            outputValid = true
            outputValidationText = "통과"
        } else {
            print("유효성 검증 오류")
            outputValid = false
            outputValidationText = "이메일 3자, 비밀번호 5자 이상"
        }
     }
}

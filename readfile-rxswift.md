# Readfile Rxswift

_Status: Published_
_Created: 2018-11-24 09:32:44_
_Tags: iOS, Rx, swift_

<code>
let disposebag = DisposeBag()
  
  enum FileReadError: Error {
    case fileNotFound, unreadable, encodingFailed
  }
  
  func loadText(from filename: String) -> Single<String> {
    return Single.create {
      single in
      let disposable = Disposables.create()
      
      guard let path = Bundle.main.path(forResource: filename, ofType: "txt") else {
        single(.error(FileReadError.fileNotFound))
        return disposable
      }
      guard let data =  FileManager.default.contents(atPath: path) else {
        single(.error(FileReadError.unreadable))
        return disposable
      }
      guard let contents = String(data: data, encoding: .utf8) else {
        single(.error(FileReadError.encodingFailed))
        return disposable
      }
      single(.success(contents))
      
      return disposable
    }
  }
  loadText(from: "filename")
    .subscribe{
      switch $0 {
      case .success(let string):
        print(string)
      case .error(let descript):
        print(descript)
      
      }
  }
    .disposed(by: disposebag)
</code>
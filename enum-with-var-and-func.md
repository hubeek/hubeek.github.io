# Enum with var and func

_Status: Published_
_Created: 2016-06-07 04:57:19_
_Tags: swift_

<code>
public enum LanguageForGame:Int
{
    
    case All    = 1,
    Dutch       = 2,
    French      = 3,
    English     = 4,
    Spanish     = 5,
    German      = 6,
    Italian     = 7,
    Swedish     = 8,
    Danish      = 9
    
    public var createLanguageCode:String
    {
        switch self {
        case .English:
            return "en"
        case .German:
            return "de"
        case .Danish:
            return "da"
        case .Swedish:
            return "sv"
        case .Dutch:
            return "nl"
        case .Spanish:
            return "es"
        case .French:
            return "fr"
        case .Italian:
            return "it"
        case .All:
            return "*"
        }
    }
    
    public var createCultureCodeWithMinus:String
    {
        switch self {
        case .English:
            return "en-GB"
        case .German:
            return "de-DE"
        case .Danish:
            return "da-DK"
        case .Swedish:
            return "sv-SE"
        case .Dutch:
            return "nl-NL"
        case .Spanish:
            return "es-ES"
        case .French:
            return "fr-FR"
        case .Italian:
            return "it-IT"
        case .All:
            return "*"
            
        }
    }
    public var createCultureCodeWithUnderScore:String
    {
        switch self {
        case .English:
            return "en_GB"
        case .German:
            return "de_DE"
        case .Danish:
            return "da_DK"
        case .Swedish:
            return "sv_SE"
        case .Dutch:
            return "nl_NL"
        case .Spanish:
            return "es_ES"
        case .French:
            return "fr_FR"
        case .Italian:
            return "it_IT"
        case .All:
            return "*"
            
        }
    }
    
    public static func getLanguageNumberFromLanguagesForGame(langString:String)->Int
    {
        
        switch langString
        {
        case "en":
            return LanguageForGame.English.rawValue
        case "de":
            return LanguageForGame.German.rawValue
        case "da":
            return LanguageForGame.Danish.rawValue
        case "se":
            return LanguageForGame.Swedish.rawValue
        case "nl":
            return LanguageForGame.Dutch.rawValue
        case "es":
            return LanguageForGame.Spanish.rawValue
        case "fr":
            return LanguageForGame.French.rawValue
        case "it":
            return LanguageForGame.Italian.rawValue
        default:
            return LanguageForGame.All.rawValue
        }
        
    }
    
}

struct HashableSequence<T: Hashable>: SequenceType {
    func generate() -> AnyGenerator<T> {
        var i = 0
        return AnyGenerator {
            guard sizeof(T) == 1 else {
                return nil
            }
            let next = withUnsafePointer(&i) { UnsafePointer<T>($0).memory }
            if next.hashValue == i {
                i += 1
                return next
            }
            
            return nil
        }
    }
}
extension Hashable {
    static func enumCases() -> Array<Self> {
        return Array(HashableSequence())
    }
    
    static var enumCount: Int {
        return enumCases().count
    }
}

let numberOfLanguages = LanguageForGame.enumCount // 9
</code>
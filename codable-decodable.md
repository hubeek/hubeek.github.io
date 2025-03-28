# Codable Decodable

_Status: Published_
_Created: 2017-11-01 17:03:25_
_Tags: swift_

<code>

enum PlanetState:String, CodingKey {
    case UnLocked = "unlocked"
    case Locked = "locked"
    case Completed = "completed"
    case Tutorial = "tutorial"
    case ComingSoon = "comingsoon"
}


class Planet: Codable
{
    var state:PlanetState
    var order:Int
    var planetBrev:String
    var bought:Bool
    var collectableGold:Int
    
    enum CodingKeys: String, CodingKey
    {
        case state      = "state"
        case order      = "order"
        case planetBrev = "planetBrev"
        case bought     = "bought"
        case collectableGold = "collectableGold"
    }
    
    init(state: PlanetState, order: Int, planetBrev:String, bought: Bool, collectableGold:Int = -1)
    {
        self.state = state
        self.order = order
        self.planetBrev = planetBrev
        self.bought = bought
        self.collectableGold = collectableGold
    }
    
    required init(from decoder: Decoder) throws {
        
        let values = try decoder.container(keyedBy: CodingKeys.self)
        self.state = (try PlanetState(rawValue: values.decode(String.self, forKey: CodingKeys.state)))!
        self.order = try values.decode(Int.self, forKey: CodingKeys.order)
        self.planetBrev = try values.decode(String.self, forKey: CodingKeys.planetBrev)
        self.bought = try values.decode(Bool.self, forKey: CodingKeys.bought)
        self.collectableGold = try values.decode(Int.self, forKey: CodingKeys.collectableGold)
    }
    
    public func encode(to encoder: Encoder) throws {
        var container = encoder.container(keyedBy: CodingKeys.self)
        try? container.encode(self.state.stringValue, forKey: CodingKeys.state)
        try? container.encode(self.order, forKey: CodingKeys.order)
        try? container.encode(self.planetBrev, forKey: CodingKeys.planetBrev)
        try? container.encode(self.bought, forKey: CodingKeys.bought)
        try? container.encode(self.collectableGold, forKey: CodingKeys.collectableGold)
    }
}
</code>
load
<code>
do {
   let planet = try decoder.decode(Planet.self, from: pData)
   HLog.info(function: #function, message: "planet \(planet.planetBrev) \(planet.collectableGold)")
   self.planets.append(planet)
 } catch {
    print("error \(error)")
 }
 </code>
save to default for example
<code>
if let jsonData = try? encoder.encode(planet)
            {
                defaults.set(jsonData, forKey: "\(Constants.kQuarkPlanetSave)\(planet.planetBrev)")
                HLog.info(function: #function, message: "defaults did save data \(planet.planetBrev)")
                savedPlanets.append(planet.planetBrev)
            }
</code>
<code>
class Excercise: Encodable,Decodable {
    var date:Date
    var remarks:[String]
    
    init(date:Date,remarks:[String]) {
        self.date = date
        self.remarks = remarks
    }
  
}

let x = Excercise(date:Date(),remarks:["avc","def"])
let encoder = JSONEncoder()
let jsonData = try encoder.encode(x)
String(data: jsonData, encoding: .utf8)!//"{"date":531262938.28764498,"remarks":["avc","def"]}"
let decoder = JSONDecoder()
let decoded = try decoder.decode(Excercise.self, from: jsonData)
decoded.date//"Nov 1, 2017 at 10:01 PM"
decoded.remarks//["avc", "def"]
type(of: decoded)//Excercise.Type
</code>
# playground network request

_Status: Published_
_Created: 2018-09-25 10:55:25_
_Tags: swift_

do not forget:
<p>import PlaygroundSupport

PlaygroundPage.current.needsIndefiniteExecution = true
</p>
<code>
    func getAll(completion: @escaping (GetResourcesRequest<ResourceType>)->Void)
    {
        let dataTask = URLSession.shared.dataTask(with: resourceURL) {

            data , _, _ in
            //print("datatask \(data) b \(b) c \(c)")
            guard let jsonData = data else {
                completion(.failure)
                return
            }
            do {
                let resources = try JSONDecoder().decode([ResourceType].self, from: jsonData)
                completion(.success(resources ))
            }
            catch {
                completion(.failure)
            }
        }
        dataTask.resume()
    }

</code>
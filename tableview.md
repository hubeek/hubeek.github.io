# tableview

_Status: Published_
_Created: 2019-05-03 10:14:53_
_Tags: iOS, swift, UIKit_

<code>
//
//  TableViewController.swift
//  SwipeActions
//
//  An exercise file for iOS Development Tips Weekly
//  by Steven Lipton (C)2018, All rights reserved
//  For videos go to http://bit.ly/TipsLinkedInLearning
//  For code go to http://bit.ly/AppPieGithub
//

import UIKit

class TableViewController: UITableViewController {

    let rowCount = 12
    
    override func tableView(_ tableView: UITableView, trailingSwipeActionsConfigurationForRowAt indexPath: IndexPath) -> UISwipeActionsConfiguration? {
        let greenAction = UIContextualAction(style: .normal, title: "Green") { (action, view, actionPerformed) in
            self.setCell(color: .green, at: indexPath)
        }
        greenAction.backgroundColor = .green
        
        let blueAction = UIContextualAction(style: .normal, title: "Blue") { (action, view, actionPerformed) in
            self.setCell(color: .blue, at: indexPath)
        }
        blueAction.backgroundColor = .blue
        
        return UISwipeActionsConfiguration(actions: [greenAction,blueAction])
    }
    
    override func tableView(_ tableView: UITableView, leadingSwipeActionsConfigurationForRowAt indexPath: IndexPath) -> UISwipeActionsConfiguration? {
        let greenAction = UIContextualAction(style: .normal, title: "Green") { (action, view, actionPerformed) in
            self.setCell(color: .green, at: indexPath)
        }
        greenAction.backgroundColor = .green
        
        let blueAction = UIContextualAction(style: .normal, title: "Blue") { (action, view, actionPerformed) in
            self.setCell(color: .blue, at: indexPath)
        }
        blueAction.backgroundColor = .blue
        
        return UISwipeActionsConfiguration(actions: [blueAction,greenAction])
    }
    
    //A simple example of what you can do in the cell
    func setCell(color:UIColor, at indexPath: IndexPath){
        
        // I can change external things
        self.view.backgroundColor = color
        // Or more likely change something related to this cell specifically.
        let cell = tableView.cellForRow(at: indexPath )
        cell?.backgroundColor = color
    }
    
    
    //Your standard Table Delegate and Data Source methods
    override func numberOfSections(in tableView: UITableView) -> Int {
        return 1
    }
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return rowCount
    }
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        cell.textLabel?.text = String(format:"Row #%i",indexPath.row + 1)
        cell.textLabel?.font = UIFont(name: "GillSans-Bold", size: 26)
        return cell
    }
    
    override func tableView(_ tableView: UITableView, titleForHeaderInSection section: Int) -> String? {
        return "Sample Action Table"
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view, typically from a nib.
    }
}

</code>
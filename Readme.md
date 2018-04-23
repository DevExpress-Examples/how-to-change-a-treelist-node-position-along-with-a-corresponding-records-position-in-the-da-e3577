# How to change a TreeList node position along with a corresponding record's position in the database


<p>TreeList allows users to reorder nodes by dragging them with the mouse. If a node was moved from one parent to another, its position will be saved automatically, because it depends on the ParentID column value which is stored in the database. However, when nodes are reordered within the child collection, their position will be reset after the application is closed and opened again, or after reloading data.</p><p>To keep nodes positions, it is necessary to add additional column to the datasource to store the node index. In this situation, nodes positions can be restored after loading the data into the TreeList. This task can be accomplished by iterating all the nodes and updating the node index via the <a href="http://documentation.devexpress.com/#WindowsForms/DevExpressXtraTreeListTreeList_SetNodeIndextopic"><u>TreeList.SetNodeIndex</u></a> method.</p>

```cs
void UpdateNodesPositions(TreeListNodes nodes) {<newline/>    List<TreeListNode> ns = new List<TreeListNode>();<newline/>    foreach (TreeListNode n in nodes)<newline/>        ns.Add(n);<newline/>    foreach (TreeListNode n in ns) {<newline/>        UpdateNodesPositions(n.Nodes);<newline/>        n.TreeList.SetNodeIndex(n, Convert.ToInt32(n.GetValue("Order")));<newline/>    }<newline/>}<newline/>
```



```vb
Private Sub UpdateNodesPositions(ByVal nodes As TreeListNodes)<newline/>	Dim ns As New List(Of TreeListNode)()<newline/>	For Each n As TreeListNode In nodes<newline/>		ns.Add(n)<newline/>	Next n<newline/>	For Each n As TreeListNode In ns<newline/>		UpdateNodesPositions(n.Nodes)<newline/>		n.TreeList.SetNodeIndex(n, Convert.ToInt32(n.GetValue("Order")))<newline/>	Next n<newline/>End Sub
```

<p> </p>


<h3>Description</h3>

The signature of the&nbsp;AfterDragNode event's delegate has been changed.&nbsp;<br>TreeList's&nbsp;OptionsBehavior.DragNodes property is now obsolete. Use TreeList's&nbsp;OptionsDragAndDrop.DragNodesMode property instead.

<br/>


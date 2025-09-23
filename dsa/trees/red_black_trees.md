# Red Black Trees

## Definition

Example:

```python
class RBNode:
  def __init__(self, val):
    self.red = None
    self.parent = None
    self.val = val
    self.left = None
    self.right = None 

class RBTree:
  def __init__(self):
    self.nil = RBNode(None)
    self.nil.red = False
    self.nil.left = None
    self.nil.right = None
    self.root = self.nil

  def rotate_left(self, pivot_parent):
    if pivot_parent is self.nil or pivot_parent.right is self.nil:
        return
    pivot = pivot_parent.right
    pivot_parent.right = pivot.left
    
    if pivot.left is not self.nil:
        pivot.left.parent = pivot_parent
    pivot.parent = pivot_parent.parent
    
    if pivot_parent is self.root:
        self.root = pivot
    elif pivot_parent is pivot_parent.parent.left:
        pivot_parent.parent.left = pivot
    elif pivot_parent is pivot_parent.parent.right:
        pivot_parent.parent.right = pivot
    pivot.left = pivot_parent
    pivot_parent.parent = pivot

  def rotate_right(self, pivot_parent):
    if pivot_parent is self.nil or pivot_parent.left is self.nil:
        return
    pivot = pivot_parent.left
    pivot_parent.left = pivot.right
    if pivot.right is not self.nil:
        pivot.right.parent = pivot_parent
    pivot.parent = pivot_parent.parent
    if pivot_parent is self.root:
        self.root = pivot
    elif pivot_parent is pivot_parent.parent.right:
        pivot_parent.parent.right = pivot
    elif pivot_parent is pivot_parent.parent.left:
        pivot_parent.parent.left = pivot
    pivot.right = pivot_parent
    pivot_parent.parent = pivot

  def insert(self, val):
    node = RBNode(val)
    node.left = self.nil
    node.right = self.nil
    node.red = True
    parent = None
    current = self.root

    while current != self.nil:
      parent = current
      if node.val < current.val:
        current = current.left
      elif node.val > current.val:
        current = current.right
      else:
        return
    node.parent = parent
    if parent is None:
      self.root = node
    else:
      if node.val > parent.val:
        parent.right = node
      else:
        parent.left = node

```


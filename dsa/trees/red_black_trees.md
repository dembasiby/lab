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


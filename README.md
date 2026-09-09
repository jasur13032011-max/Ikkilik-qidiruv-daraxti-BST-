# Ikkilik-qidiruv-daraxti-BST-
Python tilida Binary Search Tree (BST) sinfining amalga oshirilishi:

Python
class TreeNode:
    """BST uchun tugun (node) sinfi."""
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


class BinarySearchTree:
    """Ikkilik qidiruv daraxti sinfi."""
    def __init__(self):
        self.root = None

    # --- INSERT (QO'SHISH) ---
    def insert(self, value):
        """Yangi qiymat qo'shish. O'rtacha vaqt: O(log n), Eng yomon: O(n)"""
        self.root = self._insert_recursive(self.root, value)

    def _insert_recursive(self, node, value):
        if node is None:
            return TreeNode(value)

        if value < node.value:
            node.left = self._insert_recursive(node.left, value)
        elif value > node.value:
            node.right = self._insert_recursive(node.right, value)
        
        return node

    # --- SEARCH (QIDIRISH) ---
    def search(self, value):
        """Qiymatni qidirish. O'rtacha vaqt: O(log n), Eng yomon: O(n)"""
        return self._search_recursive(self.root, value)

    def _search_recursive(self, node, value):
        if node is None:
            return False
        if node.value == value:
            return True
        elif value < node.value:
            return self._search_recursive(node.left, value)
        else:
            return self._search_recursive(node.right, value)

    # --- INORDER TRAVERSAL (Chap -> Tugun -> O'ng) ---
    def inorder(self):
        """Qiymatlarni o'sish tartibida qaytaradi."""
        result = []
        self._inorder_recursive(self.root, result)
        return result

    def _inorder_recursive(self, node, result):
        if node:
            self._inorder_recursive(node.left, result)
            result.append(node.value)
            self._inorder_recursive(node.right, result)

    # --- PREORDER TRAVERSAL (Tugun -> Chap -> O'ng) ---
    def preorder(self):
        result = []
        self._preorder_recursive(self.root, result)
        return result

    def _preorder_recursive(self, node, result):
        if node:
            result.append(node.value)
            self._preorder_recursive(node.left, result)
            self._preorder_recursive(node.right, result)

    # --- POSTORDER TRAVERSAL (Chap -> O meks -> Tugun) ---
    def postorder(self):
        result = []
        self._postorder_recursive(self.root, result)
        return result

    def _postorder_recursive(self, node, result):
        if node:
            self._postorder_recursive(node.left, result)
            self._postorder_recursive(node.right, result)
            result.append(node.value)
Sinov va Murakkablik Tahlili
Python
# 1. Oddiy mutanosib (Balanced) daraxt sinovdan o'tkazilishi:
bst = BinarySearchTree()
elements = [50, 30, 70, 20, 40, 60, 80]

for el in elements:
    bst.insert(el)

print("=== ODDIY BST TRAVERSAL NATIJALARI ===")
print("Inorder (o'sish tartibida):", bst.inorder())   # [20, 30, 40, 50, 60, 70, 80]
print("Preorder (ildizdan boshlab):", bst.preorder()) # [50, 30, 20, 40, 70, 60, 80]
print("Postorder (barglardan tepaga):", bst.postorder()) # [20, 40, 30, 60, 80, 70, 50]

print("\n=== QIDIRUV (SEARCH) TESTI ===")
print("40 mavjudmi?:", bst.search(40))  # True
print("90 mavjudmi?:", bst.search(90))  # False

# 2. Nomutanosib (Skewed) daraxt holati:
skewed_bst = BinarySearchTree()
# Agar elementi allaqachon tartiblangan ro'yxat bo'yicha qo'shsak:
for val in [10, 20, 30, 40, 50]:
    skewed_bst.insert(val)
Vaqt Murakkabligi Eslatmasi (Complexity Note):

O'rtacha holat (Average Case): Daraxt mutanosib bo meks bo'lsa, balandlik h=O(logn) bo'ladi. Shuning uchun insert va search amallari O(logn) vaqt oladi.

Eng yomon holat (Worst Case - Skewed Tree): Elementlar allaqachon tartiblangan tartibda kirib kelsa ([10, 20, 30, 40, 50]), daraxt ro'yxatga (LinkedList) aylanib qoladi. Balandlik h=n bo'lib, insert va search amallari O(n) vaqt talab qiladi.

Daraxt ma'lumotlar tuzilmalari bo'yicha keyingi qadamlar:

BST'dan elementni o'chirish (delete) metodini o'rganish

AVL yoki Red-Black daraxtlari orqali o'z-o'zini muvozanatlash

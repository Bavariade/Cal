import datetim
from typing imprt List, Optional

class Item:
    def __init__(self, id: int, name: str, description: str):
        self.id = id
        self.name = name
        self.description = description
        self.created_at = datetime.datetime.now()
        self.updated_at = datetime.datetime.now()

    def update(self, name: Optional[str] = None, description: Optional[str] = None):
        if name:
            self.name = name
        if description:
            self.description = description
        self.updated_at = datetime.datetime.now()

class Repository:
    def __init__(self):
        self.items: List[Item] = []

    def add_item(self, item: Item):
        self.items.append(item)
        print(f"[{datetime.datetime.now()}] Added item: {item.name} (ID: {item.id})")

    def remove_item(self, item_id: int):
        for i, item in enumerate(self.items):
            if item.id == item_id:
                removed = self.items.pop(i)
                print(f"[{datetime.datetime.now()}] Removed item: {removed.name} (ID: {removed.id})")
                return True
        print(f"[{datetime.datetime.now()}] Item with ID {item_id} not found")
        return False

    def update_item(self, item_id: int, name: Optional[str] = None, description: Optional[str] = None):
        for item in self.items:
            if item.id == item_id:
                item.update(name, description)
                print(f"[{datetime.datetime.now()}] Updated item: {item.name} (ID: {item.id})")
                return True
        print(f"[{datetime.datetime.now()}] Item with ID {item_id} not found")
        return False

    def get_item(self, item_id: int) -> Optional[Item]:
        for item in self.items:
            if item.id == item_id:
                return item
        print(f"[{datetime.datetime.now()}] Item with ID {item_id} not found")
        return None

    def list_items(self) -> List[Item]:
        print(f"[{datetime.datetime.now()}] Listing all items ({len(self.items)} total)")
        return self.items

    def search_items(self, keyword: str) -> List[Item]:
        results = [item for item in self.items if keyword.lower() in item.name.lower() or keyword.lower() in item.description.lower()]
        print(f"[{datetime.datetime.now()}] Search for '{keyword}' returned {len(results)} results")
        return results

# Example usage
if __name__ == "__main__":
    repo = Repository()
    item1 = Item(1, "Bitcoin", "A decentralized digital currency")
    item2 = Item(2, "Ethereum", "A blockchain with smart contracts")
    
    repo.add_item(item1)
    repo.add_item(item2)
    
    repo.update_item(1, description="The first and most well-known cryptocurrency")
    repo.list_items()
    search_results = repo.search_items("blockchain")
    for item in search_results:
        print(f"Found item: {item.name} - {item.description}")

class Person:
    def __init__(self, name, is_married=False):
        self.name = name
        self.is_married = is_married
        self.kids = []
        self.spouse = None

    def marry(self, partner):
        if self.is_married or partner.is_married:
            print(f"{self.name} or {partner.name} is already married.")
        else:
            self.spouse = partner
            partner.spouse = self
            self.is_married = partner.is_married = True
            print(f"{self.name} and {partner.name} are now married.")

    def has_kids(self):
        return len(self.kids) > 0

    def adopt_kid(self, child):
        if self.is_married:
            self.kids.append(child)
            if self.spouse:
                self.spouse.kids.append(child)
            print(f"{self.name} and {self.spouse.name} have adopted {child.name}.")
        else:
            print(f"{self.name} is not married, cannot adopt.")

    def show_kids(self):
        if self.has_kids():
            return [child.name for child in self.kids]
        else:
            return "No kids"

class Baby:
    def __init__(self, name, biological_parents=None):
        self.name = name
        self.biological_parents = biological_parents if biological_parents else []

    @property
    def is_step_child(self):
        if len(self.biological_parents) < 2:
            return True
        return False

    def parents(self):
        return [parent.name for parent in self.biological_parents]


# Sample Implementation
# Creating instances for parents and a baby
parent1 = Person("John")
parent2 = Person("Jane")
baby1 = Baby("Emma", [parent1])

# Marry the couple
parent1.marry(parent2)

# Check if they have kids
print(f"Do they have kids? {parent1.has_kids()}")

# Adopt a child if they don't have kids
if not parent1.has_kids():
    parent1.adopt_kid(baby1)

# Show kids
print(f"Kids of {parent1.name} and {parent2.name}: {parent1.show_kids()}")

# Check if the baby is a stepchild
print(f"Is {baby1.name} a stepchild? {baby1.is_step_child}")

# Show parents of the baby
print(f"Parents of {baby1.name}: {baby1.parents()}")

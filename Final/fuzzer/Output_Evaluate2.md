class Term:
    def __init__(self, value):
        self.value = value

    def __str__(self):
        return str(self.value)

    def __repr__(self):
        return f"Term({self.value})"

class Variable(Term):
    def __init__(self, name):
        super().__init__(name)

    def __str__(self):
        return self.value

    def __repr__(self):
        return f"Variable({self.value})"

class Lambda(Term):
    def __init__(self, var, body):
        super().__init__(f"λ{var}. {body}")

    def __str__(self):
        return self.value

    def __repr__(self):
        return f"Lambda({self.value})"

class Application(Term):
    def __init__(self, func, arg):
        super().__init__(f"({func} {arg})")

    def __str__(self):
        return self.value

    def __repr__(self):
        return f"Application({self.func}, {self.arg})"

class Environment:
    def __init__(self):
        self.variables = {}

    def get(self, var):
        return self.variables.get(var.value)

    def set(self, var, value):
        self.variables[var.value] = value

    def __str__(self):
        return str(self.variables)

    def __repr__(self):
        return f"Environment({self.variables})"

class BetaReduction:
    @staticmethod
    def reduce(term, env):
        if isinstance(term, Variable):
            return env.get(term)
        elif isinstance(term, Application):
            func = BetaReduction.reduce(term.func, env)
            arg = BetaReduction.reduce(term.arg, env)
            return Application(func, arg)
        elif isinstance(term, Lambda):
            return term
        else:
            raise ValueError("Unsupported term")

def evaluate(term, env):
    while True:
        new_term = BetaReduction.reduce(term, env)
        if new_term == term:
            return new_term
        term = new_term

def main():
    env = Environment()
    env.set(Variable("x"), Lambda(Variable("y"), Variable("y")))
    env.set(Variable("y"), Lambda(Variable("z"), Variable("z")))
    term = Lambda(Variable("x"), Application(Lambda(Variable("y"), Variable("y")), Lambda(Variable("z"), Variable("z"))))
    result = evaluate(term, env)
    print(result)

if __name__ == "__main__":
    main()

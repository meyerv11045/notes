# Dependency Inversion & Injection

- [Video](https://www.youtube.com/watch?v=2ejbLVkCndI&list=WL&index=19)
- Dependency Injection- splits creation of objects from their usage
- Dependency Inversion- using abstract classes and interfaces to better seperate the code when doing dependency injection

``` python
## No Dependency injection or inversion- very coupled code
class Authorizer_SMS():
  def authorize(self): ...
 
class PaymentProcessor:
	def pay(self, order):
    authorizer = Authorizer_SMS() # tight coupling to authorizer_sms class and its methods
    authorizer.authorize()
    if not authorizer.is_authorized():
      raise Error
    order.set_status("paid")
    
  
## Dependency Injection
class PaymentProcessor:
	def __init__(self, authorizer: Authorizer_SMS):
    self.authorizer = authorizer

  def pay(self, order):
    self.authorizer.authorize()
    if not self.authorizer.is_authorized():
      raise Error
    order.set_status("paid")

## Dependency Inversion 
class Authorizer(ABC):
  @abstractmethod
  def authorize(self):
    pass
 	@abstractmethod
  def is_authorized(self) -> bool:
    pass

  
class Authorizer_SMS(Authorizer):
  ...
 
class PaymentProcessor:
  # now supoorts multiple types of authorizers 
  # anything that inherits from the ABC and implements the necessary methods
	def __init__(self, authorizer: Authorizer):
    self.authorizer = authorizer

  def pay(self, order):
    self.authorizer.authorize()
    if not self.authorizer.is_authorized():
      raise Error
    order.set_status("paid")
```




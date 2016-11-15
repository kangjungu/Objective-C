#Objective-C 문법 공부

1. 절차식 프로그래밍과 객체지향 프로그래밍의 차이점
	* 절차식 프로그래밍 : 프로그램이 필요로 하는 기능들을 '전역적으로 구현'해두고 각각의 상황마다 적합한 메소드를 선별하여 호출하는 방식을 취한다.
	* 객체지향 프로그래밍 언어 : 프로그램을 하나의 조립된 완제품으로 보고 그것을 구성하는 부품으로 나누어 그 각각을 하나의 독립된 객체로 다룬다. 그리고 각 객체는 자신이 필요로하는 메소드를 내부에 선언하고 정의하여 필요에 따라 호출할 수 있도록 구현한다.

	
2. Objective-C의 기초
	* 메시징 문법 : 메시지를 보낸다는 것은 객체의 메소드를 호출하는 것을 의미한다.
		*  [Receiver Message]; : `Receiver` 객체의 `Message` 메소드를 호출하는 것을 의미한다. 자바 : `Receiver.Message();`
		*  [Receiver Message:23]; : `Receiver` 객체의 `Message:` 메소드. 인자 `23`
		*  [Receiver Message:23 withOptionA:23 withOptionB: 23] : 인자를 2개 이상 넘겨주는 형식. 메소드의 이름이 완전히 끝나고 난 뒤에 인자를 표기하지 않고 메소드의 이름과 인자를 번갈아 표기하는 것이다. 메소드 이름 `Message:withOptionA:withOptionB:`. 자바 `Receiver.MessageWithOptionAandOptionB(23, 23, 23);` 

	* nil 값을 가지는 클래스 인스턴스의 메소드 호출하기
	
	````
	Recatngle *anObject = nil; //nil 값을 가지는 anObject 인스턴스
	[anObject description]; // anObject의 description 메소드 호출. 
	//다른 언어에서는 런타임 에러가 나지만 Objective-c에서는 정상적인 동작으로 인식하고 처리한다. 이같은 경우 메소드 호출결과로 nil을 돌려준다.
	````
	
	* Objective-C의 데이터 타입
		* Objective-C의 기본 데이터 타입은 'id'다. 이것은 Objectvie-C가 지원하는 모든 종류의 객체들을 다룰 수 있는 범용 데이터 타입이다. 다만, 선언된 변수가 어떤 타입의 객체가 될 것인지는 실행 시점에서 동적을 정해진다. 일반적으로 `id anObject;` 으로 사용
		* Boolean 데이터 타입 : 불리언 타입으로는 `BOOL`을 사용한다. 이 데이터 타입은 `YES`와 `NO` 두가지 값을 가진다.

		````
BOOL flag = YES;
if(flag == YES){
	...
	flas = NO;
}
		````
	* Objective-C의 클래스
		* 클래스의 상속 : Objective-C는 클래스의 상속 기능을 지원한다.(단일 클래스로부터의 상속기능만 지원한다.) 
			* 상속 : 다른 클래스의 인스턴스 변수들과 메소드들을 그대로 가져와 사용할 수 있음을 의미한다.
		* NSObject 클래스 : 부모 클래스가 없는 루트 클래스인 NSOBject는 Objective-C 객체들을 위한 기본 프레임워크로, 객체 사이의 상호 작용을 정의한다. 그래서 이를 상속하는 클래스가 객체로 동작하게 하고, 런타임 시스템과 상호 동작할수 있도록 해준다. **클래스를 새로 설계할 때 NSObject를 기본적으로 상속해야 한다**
		* 메소드 오버라이딩 : 자식 클래스에서 부모클래스의 메소드를 재정의해서 사용하는 것이다. **하지만 Objective-C 에서 메소드 오버로딩은 지원하지 않는다.**
		
		~~~~
-(void)draw {
	//1. 부모 클래스의 해당 메소드를 호출한다.
	[super draw];
	//2. 새로운 기능을 추가한다.
	...
}
		~~~~
		* 클래스 생성 : `id myRectangle = [[Rectangle alloc] init];` alloc 메소드는 Rectangle 클래스의 인스턴스 변수들에 메모리를 할당하고 이를 리턴하게 된다. 그런데 이때 인스턴스 변수들은 모두 0의 값을 가지게 되므로 init 메소드를 호출하여 초기화를 수행한다.
		* 클래스의 타입
		
		~~~~
		//Rectangle 클래스로부터 인스턴스 하나 선언
		Rectangle *myRectangle = [[Rectangle alloc] init];
		//객체를 id타입 변수에 저장 
		id idRectangle = myRectangle;
		//부모 클래스인 Shape 타입의 변수에 myRectangle; 객체 저장(부모라서 가능)
		Shape *myGraphic = myRectangle;
		~~~~
		
		* 타입검사 : 이와 같은 메소드를 이용하여 현재 변수에 저장되어 있는 인스턴스가 어느 클래스에서생성된 것인지 알아낼 수 있다.
		
		~~~~
		//특정 클래스(여기서는 Shape)의 객체인지를 알아내는 기능을 수행 
		if([anObject isMemberOfClass:[Shape class]]){
			...
		}
		//특정 클래스(여기서는 Shape) 또는 그 하위에 속한 클래스의 인스턴스인지를 알나내는 기능을 수행
		if([anObject isKindOfClass:[Shape class]]){
			...
		}
		~~~~
		
		* 동일성 검사 : 서로 다른 두 객체의 관계를 검사한다.
		
		~~~~
		//실제로 같은 메모리 주소를 가리키는 동일 인스턴스인지 검사
		if(anObject1 == anObject2){
		...
		}
		//실제 두 객체가 가직 ㅗ있는 인스턴스 내의 값들이 같은지 검사. 재정의 해서 사용해야한다.
		if([anObject1 isEqual:anObject2]){
		...
		}
		~~~~
		
		* 메소드 검사 : `respondsToSelector:` 메소드는 인자로 받은 메소드가 자신을 호출하고 있는 객체내에서 정의되어 있는지 여부를 검사하는 역할을 수행

		~~~~
		id anObject = nil;
		...
		//id 타입의 인스턴스는 실제 어떠한 타입인지 알 수 없으므로 자신이 원하는 메소드를 가지고 있는지 확인하고자 사용한다.(여기서는 draw)
		if([anObject respondsToSelector:@selector(draw)]){
			...
		}
		~~~~
	
	
3. 클래스 선언 및 정의하기
	* 헤더 파일과 소스 파일의 분리 : Objective-C에서는 클래스를 작성할 때 일반적으로 인터페이스 부분(헤더)과 구현 부분(소스)을 별도의 파일로 나누어 작성한다. 헤더와 소스 파일의 이름은 내부에 정의된 클래스의 이름을 정해지며, 헤더파일은 h, 소스파일은 m 확장자를 사용한다.
	* 헤더 파일 : .h
		
		~~~~
		#import <Foundation/Foundation.h>
		//상속하고자 하는 부모클래스를 지정하는 부분.
		#import "Shape.h"
		
		//@class는 해당 클래스를 import 하지 않고 선언만 해서 사용할 수 있도록 해준다. 해당클래스의 타입만 이용할 수있고 인스턴스 변수와 메소드를 모두 이용하려면 #import를 사용해야한다.
		@class Circle;
		
		//클래스를 선언하는 부분 클래스는 @interface에서 시작해 @end 까지이다. 클래스의 이름 뒤에 부모 클래스의 이름을 지정해야하고 부모클래스를 지정할 필요가 없을 때는 NSObject를 지정한다.
		@interface Rectangle: Shape{	
			//문자열을 나타내는 타입. 클래스에서 변수를 선언하는 경우에는 이와 같이 항상 포인터 타입으로 선언하게 된다.
			NSString *name;
			//NSString 과 달리 NSInteger는 클래스가 아닌 기본 데이터 타입이기 떄문에 포인터 타입으로 선언하지 않는다. 
			NSInteger width;
			NSInteger height;
		}
		
		/*클래스의 메소드를 선언하는 부분. 클래스 메소드와 인스턴스 메소드의 두 부분으로 나뉜다.
		클래스 메소드 : 클래스의 인스턴스가 아닌, 클래스 자체로부터 호출되는 메소드. 
		ex)id myRectangle = [[Rectangle alloc] init]; 에서 alloc은 NSObject에 선언되어있으므로 메모리를 할당하고 초기화 하는 인련의 과정없이 언제든지 호출 할 수 있다. 그렇기 때문에 인스턴스 변수를 일체 사용할수 없다. 그래서 인스턴스 변수가 필요없는 기능을 구현하는데 사용된다.
		인스턴스 메소드 : setName:,setWidth:height,draw 메소드는 호출의 주체가 객체 이다. 즉 클래스의 인스턴스로부터 호출되는 메소드를 인스턴스메소드라고 한다. 
		인스턴스 메소드를 호출하려면 반드시 메모리를 할당하고 초기화를 해야한다.	
		두 메소드를 구별하는 방법 : 클래스 메소드는 맨 앞에 +, 인스턴스 메소드는 -로 시작한다.
		*/
		//리턴타입 및 각 인자의 타입은 ()로 둘러싼다. 인자를 사용할때는 그 앞에 콜론을 입력한다.
		-(NSString *)description;
		-(void)setName:(NSString *)myName
		//두 개 이상의 인자를 사용할 때 다른 언어와 달리 메소드 이름과 인자 이름을 번갈아 표시하는 것에 주의 
		-(void)setWidth:(NSInteger)myWidth height:(NSInteger)myHeight;
		-(void)draw;
		@end
		~~~~
		
	* 소스파일 : .m
	
		~~~~
		//클래스를 선언하는 헤더 파일을 포함하는 부분 
		#import "Rectangle.h"
	
		//클래스 구현이 시작되는 부분. @implementation에서 시작되어 @end에서 끝난다.
		@implementation Rectangle
	
		//헤더파일에서 선언한 메소드를 실제로 구현하는 부분. 
		-(NSString *)description{
			...
		}
	
		-(void)setName:(NSString *)myname{
		...
		}
	
		//헤더파일에서 선언한 인스턴스 변수인 width와 height를 사용한다. 즉 이 메소드를 통해 클래스 인스턴스 변수의 값을 바꿀 수 있다.
		-(void)setWidth:(NSInteger)myWidth height:(NSInteger)myHeight{
			width = myWidth;
			height = myHeight;
		}
	
		-(void)draw{
			//부모클래스의 draw 메소드가 호출되어 실행된다.(메소드 오버라이딩)
			[super draw];
			...
		}
		@end
		~~~~
		
	* 인스턴스 변수의 접근 권한 선정 : 클래스 내부의 인스턴스 변수는 세 가지 접근 권한을 가질수 있다. 지시어를 명시하지 않으면 @protected 지시어를 사용한 것으로 간주한다.
		- @private : 인스턴스 변수를 선언한 클래스에서만 접근 가능
		- @protected : 인스턴스 변수를 선언한 클래스 및 해당 클래스를 상속한 클래스에서 접근 가능(일반적으로 가장많이 사용)
		- @public : 어디에서나 접근 가능

		~~~~
		#import <Foundation/Foundation.h>
		#import "Shape.h"
		
		@class Circle;
		
		@interface Rectangle : Shape {
			@private
			NSString *name;
			@protected
			NSInteger width;
			@public
			NSInteger height;
		}
		
		-(NSString *)description;
		-(void)setname:(NSString *)myName;
		-(void)setWidth:(NSInteger)myWidth height:(NSInteger)myHeight;
		-(void)draw;
		
		@end
		~~~~














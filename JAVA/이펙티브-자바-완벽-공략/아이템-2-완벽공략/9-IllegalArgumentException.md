
# IllegalArgumentException
- 잘못된 인자를 넘겨 받았을 때 사용할 수 있는 기본 런타임 예외 (=> unchecked exception)
- 벨로그에 정리해둔 문서 : [Effective Java | #71. 필요 없는 검사 예외 사용은 피하라](https://velog.io/@bona/Effective-Java-item-71)

## 질문1. checked exception과 unchecked exception 의 차이 

### 보람 답변
- checked exception
  - 명시적인 예외 처리를 강제하기 때문에 Checked Exception이라 한다. 반드시 try ~ catch로 예외를 잡거나 throw로 호출한 메소드에게 예외를 던져야 한다.
- unchecked exception 
  - 명시적인 예외 처리를 강제하지 않기 때문에 Uncheked Exception이라고 한다.

### 선생님 
- checked exception 발생시 다시 checked exception을 던지거나 예외를 try~catch로 잡아야한다. 복구가 가능한 상황임 
  - 트랜잭션과 예외는 관련 X  

## 질문2. 간혹 메소드 선언부에 unchecked exception 을 선언하는 이유는? 

### 보람 답변 
- 문제 발생시 개발자에게 알려줌 

### 선생님 
- 클라이언트에게 명시적으로 알려주고자 할때 
- 메서드 사용시 제약사항이 있다는 것을 알려줌 
- 대부분 사용하지 않는 이유는 너무 많기 때문에 모든 것을 명시적으로 표시하지 않음 

## 질문3. checked exception 은 왜 사용할까? 

### 보람 답변 
- 예외 발생시 프로그래머가 처리해 줄 상황이 있다면 해당 예외를 사용 

### 선생님
- 강제하는 느낌, 대부분은 unchecked exception을 쓰지만 
- 그 에러가 발생했을 때 클라이언트가 **후속 작업을 해주기 원한다면 checked exception 사용** 

## 과제1. 자바의 [모든 RuntimeException 클래스](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/RuntimeException.html) 이름 한번씩 읽어보기 
- AnnotationTypeMismatchException, ArithmeticException, ArrayStoreException, BufferOverflowException, BufferUnderflowException, CannotRedoException, CannotUndoException, CatalogException, ClassCastException, ClassNotPreparedException, CMMException, CompletionException, ConcurrentModificationException, DateTimeException, DOMException, DuplicateRequestException, EmptyStackException, EnumConstantNotPresentException, EventException, FileSystemAlreadyExistsException, FileSystemNotFoundException, FindException, IllegalArgumentException, IllegalCallerException, IllegalMonitorStateException, IllegalPathStateException, IllegalStateException, IllformedLocaleException, ImagingOpException, InaccessibleObjectException, IncompleteAnnotationException, InconsistentDebugInfoException, IndexOutOfBoundsException, InternalException, InvalidCodeIndexException, InvalidLineNumberException, InvalidModuleDescriptorException, InvalidModuleException, InvalidRequestStateException, InvalidStackFrameException, JarSignerException, JMRuntimeException, JSException, LayerInstantiationException, LSException, MalformedParameterizedTypeException, MalformedParametersException, MirroredTypesException, MissingResourceException, NashornException, NativeMethodException, NegativeArraySizeException, NoSuchDynamicMethodException, NoSuchElementException, NoSuchMechanismException, NullPointerException, ObjectCollectedException, ProfileDataException, ProviderException, ProviderNotFoundException, RangeException, RasterFormatException, RejectedExecutionException, ResolutionException, SecurityException, SPIResolutionException, TypeNotPresentException, UncheckedIOException, UndeclaredThrowableException, UnknownEntityException, UnknownTreeException, UnmodifiableModuleException, UnmodifiableSetException, UnsupportedOperationException, VMDisconnectedException, VMMismatchException, VMOutOfMemoryException, WrongMethodTypeException, XPathException


## 과제2. 이 [링크](https://docs.oracle.com/javase/tutorial/essential/exceptions/runtime.html)에 있는 글을 꼭 읽으세요. 
### 요약 
- RuntimeException은 unchecked exception 이다. 이는 프로그램 전반에서 굉장히 많이 발생이 되는데 이를 함수 상단에 명시해준다면 코드의 명확성이 떨어진다. 
  - ArithmeticException(런타임예외)의 하위 클래스인 DivideByZeroException 이나 NPE는 예외 발생시 클라이언트가 예외 처리를 해주는 것을 합리적으로 기대하기 어렵다. 
- 클라이언트가 예외에서 복구해줄 것으로 예상할 수 있는 경우, checked exception 설정
- 클라이언트가 예외에서 복구하는 작업을 수행할 수 없는 경우 unchecked exception 설정

여기서 클라이언트라 하면 해당 API를 사용하는 개발자를 말하겠쥬?

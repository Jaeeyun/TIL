# Gradle(7.0 이후 ver)의 Dependencies 파해치기
- Gradle 7부터는 compile(api)을 더 이상 사용하지 않게 되었다.
    - compile -> implementation
    - testCompile -> testImplementation
    - debugCompile -> debugImplementation
    - compileOnly나 runtimeOnly는 여전히 사용가능

## CompileClasspath
- 에러없이 컴파일을 하기 위해 필요한 클래스와 jar들의 위치를 나타낸다.

- 애플리케이션은 이것만으로 잘 돌아가지는 않고 런타임에 필요한 다른 클래스와 jar이 필요할 수도 있다.

## RuntimeClasspath
- 런타임중 애플리케이션이 정상적으로 실행하기 위해 필요한 클래스들과 jar들의 위치이다.

## 예제
'''
class A{
  public static void main(String[] args){
    B b = new B();
  }
}

class B {
  public B() {
    return new C().sum();
  }
}

class C {
  public int sum(){
    return 5;
  }
}
'''

컴파일 시에는 A,B만 알면 되지만, 런타임을 위해서는 C도 알아야 한다.

## compileOnly vs runtimeOnly vs implementation
- compileOnly는 compileClasspath에만 종속성을 둔다.
  - 빌드 결과물의 사이즈가 줄어든다.
  - ex) Lombok은 컴파일 시에 getter setter등 필요한 것을 생성시키고 런타임 때에는 작동하지 않는다.
- runtimeOnly는 runtimeClasspath에만 종속성을 둔다.
  - 해당 클래스에서 코드 변경이 일어나도 컴파일을 다시 할 필요가 없다.
  - ex) DB나 로그 관련 dependency
- implementation는 두 classpath 모두에 대한 종속을 두기 때문에 복잡성을 줄일 수 있다.

## 결론
- implementation은 지정된 모듈만 가져오고 compile(api)는 상위 모듈까지 전부 가져온다.
- 동작의 여부는 같지만 compile보다는 빌드 속도가 빠르고 필요한 모듈만 가져오는 implementation을 가져오는 것이 낫다.
  - 다중 모듈 프로젝트시 하위 implementation을 사용하면 하위 모듈이 가지는 라이브러리는 상위 모듈과 공유를 하지 않기 때문에 하위 모듈 내에서만 사용 가능하다.
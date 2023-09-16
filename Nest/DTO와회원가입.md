## DTO

Data transfer Object

계충간 데이터 교환을 위한 객체이다.

- DB에서 데이터를 얻어 Service나 Controller등으로 보낼때 사용하는 객체
- Request와 Response용 DTO는 View를 위한 클래스이다.

  ```typescript
  import { IsEmail, IsNotEmpty, IsString } from 'class-validator';

  export class CatRequestDto {
    @IsEmail()
    @IsNotEmpty()
    email: string;

    @IsString()
    @IsNotEmpty()
    password: string;

    @IsString()
    @IsNotEmpty()
    name: string;
  }
  ```

해당형식으로 Class형식의 DTO을 선언한뒤 controller의 Body에 넣으면 Body에서 HttpException필터와 함께 자등으로 Validation 된다(?)

service 계층에서 DI를 통해 DTO를 주입받아 Dto를 사용할 수 있다. 

회원가입을 받을 때 암호화를 위해 bycrypt를 사용할 수 있다.
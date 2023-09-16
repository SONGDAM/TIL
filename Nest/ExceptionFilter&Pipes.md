## Nest의 예외처리

Nest는 기존의 Express와 Exception을 처리하는 방법이 다르고 편리하게 구성되어있다.
Express에서는 `throw new error()`로 처리하지만 Nest에서는 `throw new HttpException`으로 처리할 수 있다.

<br>

<img src='https://docs.nestjs.com/assets/Filter_1.png' width='300'>

하지만 매 코드에 에외처리를 할때 똑같은 코드를 반복할 수 없으므로 filter를 만들어서 처리하는 게 효율적이다.

```typescript
import { ExceptionFilter, Catch, ArgumentsHost, HttpException } from '@nestjs/common';
import { Request, Response } from 'express';

@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();
    const status = exception.getStatus();

    response.status(status).json({
      statusCode: status,
      timestamp: new Date().toISOString(),
      path: request.url,
    });
  }
}
```

exception filter를 만들고 예외처리를 할때 라우팅 데코레이터(?) 밑에 @useFilter(HttpExceptionFilter)를 처리하거나 Global로 처리하고 싶을때는 해당 @controller 데코레이터 밑에 명시하면 된다.

실행순서는 middleware => controller => service => exception

## Pipe

<br>
<img src='https://docs.nestjs.com/assets/Pipe_1.png'>

Pipe는 두 가지의 역할이 있다. 하나는
변환과 validation인데 간단한 사례를 들면 특정 엔드포인트에 요청이 왔을때 parmeter를 특정 자료형으로 변환하는 로직을 간단한 한줄의 코드와 함께 짤 수 있다.

또한 이경우 요청이 왔을때 유효성 검사도 pipe가 도와준다.

단순히 parameter를 검사하고 변환하는 역할의 pipe도 있지만

ValidationPipe
ParseIntPipe
ParseFloatPipe
ParseBoolPipe
ParseArrayPipe
ParseUUIDPipe
ParseEnumPipe
DefaultValuePipe
ParseFilePipe

등의 여러가지 파이프도 있다.

## Pipe의 정의

파이프는 단방향 통신을 위한 용도로 사용된다. 하나의 파이프는 이전 파이프에서 전달된 결과를 입력 값으로 받아 또 다른 결과 값을 내놓는다

파이프는 클라이언트 요청에서 들어오는 데이터를 유효성 검사및 변환을 수행하여 서버가 원하는 데이터를 얻을 수 있도록 도와주는 클래스다.

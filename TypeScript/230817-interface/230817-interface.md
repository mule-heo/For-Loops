# 8월 17일 목요일 interface

1. 실습링크 https://codesandbox.io/s/interfaces-ctqw1?file=/src/index.ts:0-87

    실습링크를 열고 ButtonProps 타입 interface로 정의해주세요.

    ```
    interface ButtonProps {
        text: string;
        onClick: () => void;
    }

    const buyButton: ButtonProps = {
        text: "Buy",
        onClick: () => console.log("Buy")
    };
    ```

    답: interface ButtonProps를 추가합니다. ButtonProps는 string 타입의 text, 0개의 인자를 전달받아 void를 반환하는 함수인 onClick을 가집니다.

2. onClick을 옵션 가능하도록 만들고, buyButton의 onClick을 삭제해보세요.

    ```
    interface ButtonProps {
        text: string;
        onClick?: () => void;
    }

    const buyButton: ButtonProps = {
        text: "Buy",
    };
    ```

    답: onClick의 타입을 정의할 때 물음표를 붙여 필수가 아님을 나타냅니다.

3. extends 구문을 사용해 새로운 타입을 만들어주세요. (`interface ColoredButtonProps extends ButtonProps`)

    예시 코드도 알려주세요.

    ```
    interface ButtonProps {
        text: string;
        onClick: () => void;
    }

    interface ColorButtonProps extends ButtonProps {
        color: string;
    }

    const buyButton: ColorButtonProps = {
        color: 'orange',
        text: "Buy",
        onClick: () => console.log("Buy")
    };
    ```

    답: 이전에 정의된 ButtonProps를 extend하여 ColorButtonProps를 정의합니다. 위와 같이 정의하면 color에 대한 타입만 명시하여도 ButtonProps가 가지는 text, onClick에 대한 타입이 적용됩니다.

4. interface를 사용해 함수 타입을 정의하는 방법을 알려주세요.

    ```
    const log = (message: string) => {
      console.log(message);
    };
    ```

5. 인터페이스는 병합(declaration merging)이 가능한가요?

    답: 네. 인터페이스는 이러한 재선언을 통한 병합을 지원합니다. declaration merging이란 동일한 이름으로 재선언했을 때에 기존의 내용에 더하여 새롭게 선언한 내용이 추가되는 형태를 말합니다. 동일한 파일 내에서 동일한 이름으로 여러 번 재선언하는 것은 가독성이 떨어지고 유지보수도 어렵게 되지만 외부에서 정의된 타입의 일부를 수정하여 활용할 때 유용합니다.

    eslint 설정으로 재선언을 제한하는 규칙(no-redeclare)을 적용하였다면 재선언을 하였을 때 경고 메시지 또는 오류를 출력합니다.

    동일한 파일 내에서 인터페이스를 여러 번 재선언하는 경우 동일한 속성에 대하여 동일한 타입을 지정하여야 합니다. 서로 다른 타입을 지정하고자 하는 경우 오류가 발생합니다. 인터페이스를 외부로부터 가져오는 경우에만 동일한 속성에 대하여 다른 타입을 지정할 수 있습니다. 동일한 파일 안에서 같은 속성에 대하여 서로 다른 타입을 지정하는 것은 논리적인 오류라고 보는 것이 맞을 것 같습니다.

    ```
    // 오류가 발생합니다.

    interface ButtonProps {
        text: string;
    }
    interface ButtonProps {
        text: number;
    }
    ```

    ```
    // 오류가 발생하지 않습니다.

    // somewhere.ts
    export interface ButtonProps {
        text: string;
    }

    // index.ts
    import { ButtonProps } from './somewhere';

    interface ButtonProps {
        text: number;
    }
    ```


출제 레퍼런스: https://learntypescript.dev/04/l4-interfaces
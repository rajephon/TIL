# Formik / Yup 사용하기

- `initialvalues`, `onSubmit`, `validationSchema`를 이용하여 제어
- antd에서 값 연결은 `input onChange`에 `formik.setFieldValue`를 연결하여 사용
- 유효성 검사 결과는 `formik.errors.`에서 확인

```typescript
import React from 'react';
import { Formik } from 'formik';
import * as Yup from 'yup';

const MIN_SUBJECT_LENGTH = 3;
const MAX_SUBJECT_LENGTH = 20;

const sample = () => {
    const initValues:Foo = {
        subject: '',
        article: '',
    }

    const onSubmit = (values: Foo, {setSubmitting}: FormikHelpers<Foo>) => {
        setSubmitting(false);
    };

    return (
        <Formik initialValues={initValues}
            onSubmit={onSubmit}
            validationSchema={Yup.object({
                subject: Yup.string().min(MIN_SUBJECT_LENGTH, `제목은 ${MIN_SUBJECT_LENGTH}글자 이상으로 작성해주세요.`).max(MAX_SUBJECT_LENGTH, `제목은 ${MAX_SUBJECT_LENGTH}자 이내로 작성해주세요.`).required('제목을 입력해주세요.'),
            })}
        >
            {formik => (
                <Form
                    onFinish={formik.handleSubmit}
                >
                    <Form.Item label="제목" name="subject"
                        validateStatus={formik.touched.subject && formik.errors.subject ? 'error' : undefined}
                        help={formik.touched.subject && formik.errors.subject}
                    >
                        <Input onChange={(value) => formik.setFieldValue('subject', value.currentTarget.value)} />
                    </Form.Item>
                    <Form.Item>
                        <Button type="primary" htmlType="submit" size="large" block>
                        등록
                        </Button>
                    </Form.Item>
                </Form>
            )}
        </Formik>
    )

};

```

## Reference
- [리액트(React) Formik / Yup - roh160308](https://velog.io/@roh160308/%EB%A6%AC%EC%95%A1%ED%8A%B8React-Formik-Yup)

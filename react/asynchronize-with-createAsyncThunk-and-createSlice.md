# createAsyncThunk와 createSlice를 사용하여 비동기 처리하기

비동기 작업을 효율적으로 처리하기 위해 `Redux Toolkit`은 `createAsyncThunk`과 `createSlice`라는 강력한 도구를 제공합니다. 이 두 함수를 함께 사용하면 비동기 작업을 처리하고 상태를 업데이트하기 위한 코드를 간편하게 작성할 수 있습니다.

<br>

## createAsyncThunk

`createAsyncThunk`는 비동기 작업을 처리하는 `Thunk` 액션 생성자를 생성하는 데 사용됩니다. 비동기 작업은 주로 API 호출과 같은 외부 데이터 소스와의 상호 작용에 사용됩니다.

```js
export const fetchSearchResults = createAsyncThunk(
    'search/fetchSearchResults',
    async (searchTerm) => {
        try {
            const response = await axios.get(
                `https://api.datamuse.com/words?rel_rhy=${searchTerm}`
            );
            return response.data;
        } catch (error) {
            throw error;
        }
    }
);
```

`createAsyncThunk`는 필수적으로 다음 두 가지의 인자를 가집니다.

- **action:** 문자열로 사용자 임의로 설정
- **payloadCreator:** 콜백 함수(비동기 처리를 위한 로직을 가지는 함수)

<br>

## createSlice

`createSlice`는 리듀서와 액션을 함께 정의하여 `Redux` 스토어를 업데이트하는데 사용됩니다. 이를 통해 보일러플레이트 코드를 크게 줄일 수 있습니다.

```js
const searchSlice = createSlice({
    name: 'search',
    initialState: {
        searchTerm: '',
        searchResults: [],
        status: 'idle', // 추가된 상태
        error: null, // 추가된 상태
    },
    reducers: {
        setSearchTerm: (state, action) => {
            state.searchTerm = action.payload;
        },
    },
    extraReducers: (builder) => {
        builder
            .addCase(fetchSearchResults.pending, (state) => {
                state.status = 'loading';
                state.error = null;
            })
            .addCase(fetchSearchResults.fulfilled, (state, action) => {
                state.status = 'succeeded';
                state.searchResults = action.payload;
            })
            .addCase(fetchSearchResults.rejected, (state, action) => {
                state.status = 'failed';
                state.error = action.error.message;
            });
    },
});
```

- **name:** 해당 모듈의 이름을 작성합니다.
- **initialState:** 해당 모듈의 초기값을 세팅합니다.
- **reducer:** 리듀서를 작성한다. 이때 해당 리듀서의 키값으로 액션 함수가 자동으로 생성합니다.

<br>

> `pending`, `fulfilled`, `rejected`는 `Redux Toolkit`의 `createAsyncThunk`에서 생성된 비동기 액션에 대한 상태들을 나타냅니다. 이 세 가지 상태는 주로 비동기 작업의 성공, 실패, 혹은 진행 중인 상태를 나타내기 위해 사용됩니다.

# contextについて
- getStaticProps/getServerSideProps/getInitialPropsの引数に渡される。
- リクエスト情報などが格納されている。

# getStaticPropsで渡されるcontextの代表的なプロパティ
    - params
        - パスパラメータが格納されている。
    - locale
        - ロケール情報が格納されている。
    - locales
        - ロケール情報の一覧が格納されている。
    - defaultLocale
        - デフォルトのロケール情報が格納されている。
    - preview
        - プレビューモードか？
    - previewData
        - Preview ModeでsetPreviewDataによってセットされたデータが格納されている。
        
# getServerSidePropsで渡されるcontextの代表的なプロパティ
    - req
        - リクエスト情報が格納されている。
    - res
        - レスポンス情報が格納されている。
    - query
        - クエリパラメータが格納されている。
    - resolvedUrl
        - リクエストされたURLが格納されている。
Title: Verify that an ID is both a valid integer and exists in a given table?
Date: 2021-08-30 10:48:00
Category: General


SELECT
    CASE WHEN EXISTS 
    (
        SELECT CompNo FROM dbo.Companies WHERE CompNo = TRY_CONVERT(smallint, @companyId)
    )
    THEN 1
    ELSE 0
END

# Improve Code Quality

* Use meaningfull nameing
  * [Google Coding Style Naming](https://google.github.io/styleguide/cppguide.html#Naming)
  * File Name
    * `name_like_this.cpp`
  * Type Name

    ```C++
    // classes and structs
    class UrlTable1 {...}
    class UrlTableTest {...}
    struct struct UrlTablePropertie {...}

    // typedefs
    typedef hash_map<UrlTableProperties *, std::string> PropertiesMap;

    // using aliases
    using PropertiesMap = hash_map<UrlTableProperties *, std::string>;

    // enums
    enum class UrlTableError { ...
    ```

  * Variable Name
    * Common Variable Name

      ```C++
      std::string table_name;  // OK - lowercase with underscore.
      std::string tableName;   // Bad - mixed case.
      ```

  * Class Data Members
    * with a ***trailing underscore***

      ```C++
      class TableInfo {
        ...
      private:
        std::string table_name_;  // OK - underscore at end.
        static Pool<TableInfo>* pool_;  // OK.
      };
      ```

  * Struct Data Members
    * DONT need underscore
  * Constant Names
    * Leading with k...
    * Example: `const int kDaysInAWeek = 7;`
  * Enumerator Names

    ```C++
    enum class UrlTableError {
      kOk = 0,
      kOutOfMemory,
      kMalformedInput,
    };
    ```

  * Function
    * With mix cases
    * Example: `AddOne()`, `CheckSum`
  * 



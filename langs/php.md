# PHP

## Code
- **Follow the [PSR-2](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md) coding guidelines**, with the following exceptions:

    - underscore_case is ok for naming variables and functions if you prefer it to camelCase (it’s arguably [easier to read](https://whathecode.wordpress.com/2013/02/16/camelcase-vs-underscores-revisited/)), but if you use it, don't mix with camelCase (ie. choose one and use it consistently).
    - Opening curly brackets may always be on a new line. eg: 

        ```php
        if ($status === 3)
        {
           ...
        }
        ```
    - Consistency of coding style within a project is more important than adhering to any coding standard. If you’re working with an existing project or framework, use its existing style.
- **Use strict comparison** (identity) operators (=== and !==) rather than loose comparison (equality) operators (== and !=) wherever possible.
    - This avoids tricky-to-spot bugs that can creep in when things unexpectedly get treated as equivalent. eg. `0` is often not the same as `false` or `null`: for example, [strpos](http://php.net/manual/en/function.strpos.php) can return either `0` (first character of the string matches) or `false` (no match) - but if you compare them with == a match at position `0` may be treated as no match.
 
## Testing
- **Use a test-driven approach** for code of any complexity. Use [PHPUnit](https://phpunit.de/) for testing.

## Comments
- **Comment everything** non-trivial (and even trivial things, if you like). Be clear, and as verbose as you like. Over-commenting is better than under-commenting. Write for your future self as much as anyone else. Ideally, it should be possible to get a good idea of what the code does by reading through the comments alone.
- **For methods and functions, use [docblock](http://www.phpdoc.org/docs/latest/references/phpdoc/index.html)-style comments** to give an overview of the function's purpose, arguments, and return values.
- **Inline comments which explain code should start with //**. In a perfect world, every significant chunk of code would be preceded by a // comment.
- **More general comments should start with ##** (eg. notes to self / placeholder comments / to-do items, etc). Avoid writing too many of these sorts of comments, but where they're necessary use ## so they stand out from explanatory comments. As a rough guide ## comments are ones that ideally will be removed at some point in the future.

Here's some pseudo-code to illustrate some of the above points: 

```php
/**
 * Get a number of Widgets, optionally filtered by status
 *
 * @param int   $count  Number of Widgets to return
 * @param int   $status Status to filter by
 *
 * @return array    Array of Widget objects
 */
 public function getWidgets($number = 10, $status = null)
 {
    // Start building the database query:
    $query = DB::select()->from('widgets');
    
    ## TO DO: cache the results, so we don't have 
    ## to query the DB every time?
    
    // If a status was specified, add it to the query:
    if ($status !== null)
    {
        $query->where('status', '=', $status);
    }
    
    // Limit the results to the required number of Things:
    $query->limit($number);
    
    // Execute the query and return the response as an array of Things:
    return $query->asObject('Widget')->execute();
 }
```

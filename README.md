initial commit: Answered questions from conceptual.md.


what test functions to add to timeWord?
    - testing invalid input time
    - noon
    - midnight
    - returns time inputted

several bugs in the bankly app:
    1. Cannot register using the register route because it uses SELECT instead of INSERT INTO, problem below:
          static async register({username, password, first_name, last_name, email, phone}) {
    const duplicateCheck = await db.query(
      `SELECT username 
        FROM users 
        WHERE username = $1`,
      [username]
    );
    Implemented a fix using INSERT INTO.

2. Bug here, not returning the username and password req.body
 static async getAll(username, password) {
    //second bug, 
    const result = await db.query(
      `SELECT username,
                first_name,
                last_name,
                email,
                phone
            FROM users 
            ORDER BY username`, [username, password]
    );
    return result.rows;

3. To delete a user, only admins can do it, but since we have "authUsers" that allows users to do it, I'll delete users.
  router.delete('/:username', requireAdmin, async function(
  req,
  res,
  next
) {
  try {
    User.delete(req.params.username);
    return res.json({ message: 'deleted' });
  } catch (err) {
    return next(err);
  }


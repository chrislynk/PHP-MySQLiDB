<?php
/*
# This file is part of MySQLi-Class.
#
# Copyright(c) 2014 Giacomo Cerquone
# cerquone96@hotmail.it
# http://www.giacomocerquone.it
#
# This file may be licensed under the terms of of the
# GNU General Public License Version 2 (the ``GPL'').
#
# Software distributed under the License is distributed
# on an ``AS IS'' basis, WITHOUT WARRANTY OF ANY KIND, either
# express or implied. See the GPL for the specific language
# governing rights and limitations.
#
# You should have received a copy of the GPL along with this
# program. If not, go to http://www.gnu.org/licenses/gpl.html
# or write to the Free Software Foundation, Inc.,
# 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301, USA.
*/

  class mysqliDB {
    private $conn = false,           //Boolean for the connection state
            $mysqli,                 //Mysqli istance
            $host, $pwd, $usr, $db;  //DB information

    public function __construct($host, $usr, $pwd, $db) {
      $this->host = $host;
      $this->usr = $usr;
      $this->pwd = $pwd;
      $this->db = $db;
    }

    //CONNECT to the database
    public function Connect() {

      //If it's already connected return true
      if($this->conn)
        return true;

      //Otherwise connect to the db through mysqli class
      $this->mysqli = new mysqli($this->host, $this->usr, $this->pwd, $this->db);

      //If there are no errors
      if(!$this->mysqli->connect_errno) {

        //Set the boolean var to true (connected)
        $this->conn = true;
        return true;
      }

      //Otherwise the function return false
      return false;
    }

    //DISCONNECT from the database
    public function Disconnect() {

      //If it's already not connected return true
      if(!$this->conn)
        return true;

      //If there aren't problems closing the connection return true
      if($this->mysqli->close()) {
        return true;
      }

      //Otherwise return false
      return false;
    }

    //Perform a query on the database
    public function Query($query) {
      if(!$this->conn)
        $this->Connect();
      
      //If there aren't problems executing the query return true
      if($exe = $this->mysqli->query($query))
        return $exe;

      return false;
    }
    
    //Perform a query and get the result rows
    public function GetRows($query) {
      if(!$exe = $this->Query($query))
        return false;

      $rows = array();
      //Every row is pushed into the array as an associative array
      while($tmp = $exe->fetch_assoc()) {
              $rows[] = $tmp;
      }
      return $rows;

    }
  
    //Insert a row into a specified table
    public function InsertRow($table, $data) {
      //Take the keys of the associative array composed by the keys (the columns of the db) and the values (the values to put into the row)
      $fields = array_keys($data);
      if($this->Query("INSERT INTO ".$table. "(". implode(",", $fields). ") VALUES ('".implode("','", $data)."');"))
        return true;
      
      return false;
    }

  }
?>
